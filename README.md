#!/usr/bin/env python3

import os

def run_cmd(cmd):
    """Runs a shell command and prints it."""
    print(f"\n> {cmd}")
    os.system(cmd)

def dir_exists(path):
    """Checks if a given directory path exists."""
    return os.path.isdir(path)

def main():
    print("=== EFS Automation Script (Dev/Prod) ===")

    # Ask the user for environment
    mode = input("Enter environment (dev/prod): ").strip().lower()
    if mode not in ["dev", "prod"]:
        print("Invalid input. Must be 'dev' or 'prod'.")
        return

    # Define constants
    metaproject = "starburst"  # Fixed for this setup
    project = input("Enter project name (e.g., trinob): ").strip()
    release = input("Enter release version (e.g., 42): ").strip()

    # Define cell based on environment
    cell = "d-usw2850.chi.amrs.ml.com" if mode == "dev" else "d.uspa01.nyc.amrs.ml.com"
    
    # Define base install path
    base_path = f"/efs/{mode}/{metaproject}/{project}/{release}/install/common"

    # Step 1: Create project (only if it doesn't already exist)
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}"):
        run_cmd(f"efs create project {metaproject} {project} {cell}")
    else:
        print(f"[SKIP] Project already exists: {project}")

    # Step 2: Create release if needed
    if not dir_exists(f"/efs/{mode}/{metaproject}/{project}/{release}"):
        run_cmd(f"efs create release {metaproject} {project} {release}")
    else:
        print(f"[SKIP] Release already exists: {release}")

    # Step 3: Create install directory
    if not dir_exists(base_path):
        run_cmd(f"efs create install {metaproject} {project} {release} common")
    else:
        print(f"[SKIP] Install directory already exists: {base_path}")

    # Step 4: Copy files to EFS path
    print("\nEnter full file paths to upload (comma-separated):")
    files = input("Files: ").strip().split(',')
    for file in files:
        file = file.strip()
        if file:
            run_cmd(f"cp {file} {base_path}")

    # Step 5: Finalize release
    run_cmd(f"efs checkpoint release {metaproject} {project} {release}")
    run_cmd(f"efs dist release {metaproject} {project} {release} --celltype {mode} --global")

    # Output results
    print("\n=== SUCCESS ===")
    print(f"{mode.upper()} EFS setup completed.")
    print(f"EFS Path: {base_path}")

    # Final message for sharing
    print("\n--- Copy & Share Message ---")
    print(f"{mode.upper()} EFS setup for {project} v{release} completed successfully.")
    print(f"Files available at: {base_path}")

if __name__ == "__main__":
    main()
