import os
import shutil
import requests
from datetime import datetime, timedelta
import ctypes

# === CONFIGURATION ===
SHARE_PATH = r"G:\\"  # Update as per your drive
LIMIT_GB = 1  # Alert when usage crosses 1 GB
DELETE_AFTER_DAYS = 30  # Delete files older than this
NOTIFY_BEFORE_DAYS = 2  # Notify before deletion
MATTERMOST_WEBHOOK = "https://your_mattermost_webhook_url"
ARCHIVE_BEFORE_DELETE = True
ARCHIVE_PATH = r"G:\archive\\"
DRY_RUN = False  # True = simulate deletion only

# === FUNCTION DEFINITIONS ===

def get_usage(path):
    total, used, free = shutil.disk_usage(path)
    return total / (1024**3), used / (1024**3), free / (1024**3)

def send_mattermost_alert(message):
    payload = {"text": message}
    try:
        response = requests.post(MATTERMOST_WEBHOOK, json=payload)
        if response.status_code != 200:
            print("Mattermost alert failed.")
    except Exception as e:
        print(f"Error sending Mattermost alert: {e}")

def popup_message(message):
    ctypes.windll.user32.MessageBoxW(0, message, "Storage Alert", 1)

def check_usage_and_alert():
    total, used, free = get_usage(SHARE_PATH)
    print(f"Total: {total:.2f} GB, Used: {used:.2f} GB, Free: {free:.2f} GB")

    if used > LIMIT_GB:
        alert_msg = f"⚠️ Share usage alert! Used: {used:.2f} GB (Limit: {LIMIT_GB} GB)"
        send_mattermost_alert(alert_msg)
        popup_message(alert_msg)

def archive_file(file_path):
    if not os.path.exists(ARCHIVE_PATH):
        os.makedirs(ARCHIVE_PATH)
    shutil.move(file_path, ARCHIVE_PATH)

def delete_old_files():
    cutoff_date = datetime.now() - timedelta(days=DELETE_AFTER_DAYS)
    notify_date = datetime.now() - timedelta(days=DELETE_AFTER_DAYS - NOTIFY_BEFORE_DAYS)
    
    files_to_delete = []
    for root, _, files in os.walk(SHARE_PATH):
        for name in files:
            file_path = os.path.join(root, name)
            try:
                modified_time = datetime.fromtimestamp(os.path.getmtime(file_path))
                if modified_time < cutoff_date:
                    files_to_delete.append(file_path)
                elif modified_time < notify_date:
                    send_mattermost_alert(f"⏰ File `{file_path}` will be deleted in {NOTIFY_BEFORE_DAYS} days.")
            except Exception as e:
                print(f"Error checking file: {file_path}, {e}")

    if not files_to_delete:
        print("No files to delete.")
        return

    print("\nFiles scheduled for deletion:")
    for f in files_to_delete:
        print(f)

    confirm = input("\nProceed with deletion? (yes/no): ").strip().lower()
    if confirm == "yes":
        for f in files_to_delete:
            try:
                if DRY_RUN:
                    print(f"[Dry Run] Would delete: {f}")
                else:
                    if ARCHIVE_BEFORE_DELETE:
                        archive_file(f)
                        print(f"Archived: {f}")
                    else:
                        os.remove(f)
                        print(f"Deleted: {f}")
            except Exception as e:
                print(f"Error deleting {f}: {e}")
    else:
        print("Deletion canceled by user.")

# === MAIN EXECUTION ===
if __name__ == "__main__":
    print("==== Storage Automation Started ====")
    check_usage_and_alert()
    delete_old_files()
    print("==== Process Completed ====")
