#!/usr/bin/env python3

import os

def run_cmd(cmd):
    """Run and show shell command output."""
    print(f"\n> {cmd}")
    os.system(cmd)

def dir_exists(path):
    """Check if a directory exists."""
    return os.path.isdir(path)

def list_releases(project):
    """List releases for a given project."""
    output = os.popen(f"efs list release starburst {project}").read()
    releases = []
    for line in output.splitlines():
        parts = line.strip().split()
        if len(parts) >= 3 and parts[0] == "starburst" and parts[1] == project:
            releases.append(parts[2])
    return releases

def create_release_flow():
    """Create a new EFS release and upload files."""
    print("\n=== EFS Create & Upload Tool ===")
    mode = input("Enter environment (dev/prod): ").strip().lower()
    if mode not in ["dev", "prod"]:
        print("Invalid input. Must be 'dev' or 'prod'.")
        return

    metaproject = "starburst"
    project = input("Enter project name (e.g., trinob): ").strip()
    release = input("Enter release version (e.g., 42): ").strip()

    dev_cell = "d-usw2850.chi.amrs.ml.com"
    prod_cell = "d.uspa01.nyc.amrs.ml.com"
    cell = dev_cell if mode == "dev" else prod_cell

    base_path = f"/efs/{mode}/{metaproject}/{project}/{release}/install/common"

    # Create project if not exists
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}"):
        run_cmd(f"efs create project {metaproject} {project} {cell}")
    else:
        print(f"[SKIP] Project already exists: {project}")

    # Create release if not exists
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}/{release}"):
        run_cmd(f"efs create release {metaproject} {project} {release}")
    else:
        print(f"[SKIP] Release already exists: {release}")

    # Create install directory if not exists
    if not dir_exists(base_path):
        run_cmd(f"efs create install {metaproject} {project} {release} common")
    else:
        print(f"[SKIP] Install path already exists: {base_path}")

    # Upload files
    print("\nEnter full file paths to upload (comma-separated):")
    files = input("Files: ").strip().split(",")
    for file in files:
        file = file.strip()
        if file:
            run_cmd(f"cp {file} {base_path}")

    # Finalize release
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
    """Delete EFS release and then project."""
    print("\n=== EFS Release & Project Deletion Tool ===")
    run_cmd("efs list project starburst")
    project = input("\nEnter the project you want to delete (e.g., trinob): ").strip()

    releases = list_releases(project)
    if not releases:
        print(f"No releases found for project '{project}'. Proceeding to project delete...")
    else:
        print(f"Releases found for project '{project}': {', '.join(releases)}")
        release = input("Enter the release version to delete: ").strip()
        confirm = input(f"\n[WARNING] This will DELETE release and project from EFS.\n"
                        f"You're deleting project: {project}, release: {release}\n"
                        f"Type 'DELETE' to confirm: ").strip()
        if confirm == "DELETE":
            run_cmd(f"efs purge release starburst {project} {release}")
            run_cmd(f"efs destroy release starburst {project} {release}")
        else:
            print("Aborted.")
            return

    # Attempt to delete the project now
    run_cmd(f"efs destroy project starburst {project}")
    print("\n=== CLEANUP COMPLETE ===")

def main():
    """Main menu."""
    print("\n========= EFS Automation =========")
    print("1. Create & Upload Files to EFS")
    print("2. Delete EFS Release and Project")
    choice = input("Choose an option (1/2): ").strip()
    if choice == "1":
        create_release_flow()
    elif choice == "2":
        delete_release_and_project()
    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()
