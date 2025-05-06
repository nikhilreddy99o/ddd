#!/usr/bin/env python3
import os

def run_cmd(cmd):
    """Run and display shell command output."""
    print(f"\n> {cmd}")
    os.system(cmd)

def dir_exists(path):
    """Check if directory exists."""
    return os.path.isdir(path)

def list_releases(project):
    """Get a list of releases for a project."""
    output = os.popen(f"efs list release starburst {project}").read()
    releases = []
    for line in output.splitlines():
        if line.strip().startswith(project):
            parts = line.split()
            if len(parts) > 2:
                releases.append(parts[2])
    return releases

def create_release_flow():
    """Create a new EFS project and upload files."""
    print("\n=== EFS Automation Script (Dev/Prod) ===")
    mode = input("Enter environment (dev/prod): ").strip().lower()
    if mode not in ["dev", "prod"]:
        print("Invalid input. Must be 'dev' or 'prod'.")
        return

    metaproject = "starburst"
    project = input("Enter project name (e.g., trinob): ").strip()
    release = input("Enter release version (e.g., 42): ").strip()

    # Dev/Prod cell
    dev_cell = "d.usw2850.nyc.amrs.ml.com"
    prod_cell = "d.uspa01.nyc.amrs.ml.com"
    cell = dev_cell if mode == "dev" else prod_cell

    base_path = f"/efs/{mode}/{metaproject}/{project}/{release}/install/common"

    # Step 1: Project
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}"):
        run_cmd(f"efs create project {metaproject} {project} {cell}")
    else:
        print(f"[SKIP] Project already exists: {project}")

    # Step 2: Release
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}/{release}"):
        run_cmd(f"efs create release {metaproject} {project} {release}")
    else:
        print(f"[SKIP] Release already exists: {release}")

    # Step 3: Install path
    if not dir_exists(base_path):
        run_cmd(f"efs create install {metaproject} {project} {release} common")
    else:
        print(f"[SKIP] Install directory exists: {base_path}")

    # Step 4: Upload files
    print("\nEnter full file paths to upload (comma-separated):")
    files = input("Files: ").strip().split(',')
    for file in files:
        file = file.strip()
        if file:
            run_cmd(f"cp {file} {base_path}")

    # Step 5: Finalize
    run_cmd(f"efs checkpoint release {metaproject} {project} {release}")
    run_cmd(f"efs dist release {metaproject} {project} {release} --celltype {mode} --global")

    # Summary
    print("\n=== SUCCESS ===")
    print(f"{mode.upper()} EFS setup completed.")
    print(f"EFS Path: {base_path}")
    print("\n--- Copy & Share Message ---")
    print(f"{mode.upper()} EFS setup for {project} v{release} completed successfully.")
    print(f"Files available at: {base_path}")

def delete_release_and_project():
    """Destroy release and project safely after confirmation."""
    print("\n=== EFS Release & Project Deletion Tool ===")
    project = input("Enter the project you want to delete (e.g., trinob): ").strip()
    releases = list_releases(project)

    if not releases:
        print(f"No releases found for project '{project}'.")
        return

    print(f"Releases found for project '{project}': {', '.join(releases)}")
    release = input("Enter the release version to delete: ").strip()

    print(f"\n[WARNING] This will permanently DELETE release and project from EFS.")
    print(f"You are deleting project: {project}, release: {release}")
    confirm = input("Type 'DELETE' to confirm: ").strip()

    if confirm == "DELETE":
        run_cmd(f"efs purge release starburst {project} {release}")
        run_cmd(f"efs destroy release starburst {project} {release}")
        run_cmd(f"efs destroy project starburst {project}")
        print("\n=== SUCCESS ===")
        print(f"Deleted release '{release}' and project '{project}'.")
    else:
        print("Aborted.")

def main():
    print("\n=== EFS Manager ===")
    print("1. Create EFS Project/Release")
    print("2. Delete EFS Release & Project")
    choice = input("Choose an option (1 or 2): ").strip()

    if choice == "1":
        create_release_flow()
    elif choice == "2":
        delete_release_and_project()
    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()
