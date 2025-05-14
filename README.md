import os
import shutil
import requests
from datetime import datetime, timedelta
import ctypes

# === CONFIGURATION ===
SHARE_PATH = "G:\\"
INIT_GB = 1  # Alert when usage crosses 1 GB
DELETE_AFTER_DAYS = 30
NOTIFY_BEFORE_DAYS = 2
MATTERMOST_WEBHOOK = "https:/hooks/your_webhook_here"
ARCHIVE_BEFORE_DELETE = True
ARCHIVE_PATH = "G:\\archive\\"
DRY_RUN = False

def get_usage(path):
    total, used, free = shutil.disk_usage(path)
    return total / (1024 ** 3), used / (1024 ** 3), free / (1024 ** 3)

def send_mattermost_alert(message, mention_all=False):
    mention = " @all" if mention_all else ""
    payload = {"text": f"{message}{mention}"}
    try:
        response = requests.post(MATTERMOST_WEBHOOK, json=payload, verify=False)
        if response.status_code != 200:
            print("Mattermost alert failed.")
    except Exception as e:
        print(f"Error sending Mattermost alert: {e}")

def popup_message(message):
    ctypes.windll.user32.MessageBoxW(0, message, "Storage Alert", 1)

def archive_file(file_path):
    try:
        if not os.path.exists(ARCHIVE_PATH):
            os.makedirs(ARCHIVE_PATH)
        shutil.move(file_path, ARCHIVE_PATH)
        send_mattermost_alert(f"📦 Archived: `{file_path}`")
    except Exception as e:
        send_mattermost_alert(f"❌ Failed to archive `{file_path}`: {e}")

def delete_old_files():
    cutoff_date = datetime.now() - timedelta(days=DELETE_AFTER_DAYS)
    notify_date = datetime.now() - timedelta(days=NOTIFY_BEFORE_DAYS)
    files_deleted = 0

    for root, _, files in os.walk(SHARE_PATH):
        for file in files:
            file_path = os.path.join(root, file)
            modified_time = datetime.fromtimestamp(os.path.getmtime(file_path))

            if modified_time < cutoff_date:
                if ARCHIVE_BEFORE_DELETE:
                    archive_file(file_path)
                if not DRY_RUN:
                    try:
                        os.remove(file_path)
                        send_mattermost_alert(f"🗑️ Deleted: `{file_path}`")
                        files_deleted += 1
                    except Exception as e:
                        send_mattermost_alert(f"❌ Error deleting `{file_path}`: {e}")
            elif modified_time < notify_date:
                send_mattermost_alert(f"⚠️ `{file_path}` will be deleted in {NOTIFY_BEFORE_DAYS} days.")

    send_mattermost_alert(f"✅ Cleanup completed. Total files deleted: **{files_deleted}**.", mention_all=True)

# === MAIN EXECUTION ===

total, used, free = get_usage(SHARE_PATH)
if used >= INIT_GB:
    alert_message = f"⚠️ Share usage alert! Used: **{used:.2f} GB**, Limit: **{INIT_GB} GB**"
    send_mattermost_alert(alert_message, mention_all=True)
    popup_message(alert_message)

delete_old_files()
