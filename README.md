#!/usr/bin/env python3

import os

def run_cmd(cmd):
    """Execute and display a shell command."""
    print(f"\n> {cmd}")
    os.system(cmd)

def list_releases(project):
    """Return list of releases for the given project."""
    # Extract release list using efs display command (simple parsing)
    stream = os.popen(f"efs display release starburst --project {project}")
    output = stream.read()
    releases = []
    for line in output.splitlines():
        parts = line.strip().split()
        if len(parts) >= 3 and parts[0] == "starburst" and parts[1] == project:
            releases.append(parts[2])
    return releases

def main():
    print("\n=== EFS Release & Project Deletion Tool ===")

    # Display existing projects
    print("\n--- Existing Projects ---")
    run_cmd("efs display project starburst")

    # Ask for project name
    project = input("\nEnter the project you want to delete (e.g., trinob): ").strip()

    # Show all releases for this project
    releases = list_releases(project)
    if not releases:
        print(f"\nNo releases found for project '{project}'.")
        return

    print(f"\nReleases found under project '{project}': {', '.join(releases)}")
    release = input(f"Enter the release you want to delete (choose from above): ").strip()

    if release not in releases:
        print(f"\nRelease '{release}' not found in project '{project}'. Aborting.")
        return

    # Confirm with user
    print(f"\n[WARNING] You are about to DELETE:")
    print(f"  Project  : {project}")
    print(f"  Release  : {release}")
    print(f"  All files and setup under this release will be lost.")
    confirm = input("Type DELETE to continue: ").strip()
    if confirm != "DELETE":
        print("Aborted by user.")
        return

    # Step 1: Purge release
    run_cmd(f"efs purge release starburst {project} {release}")

    # Step 2: Destroy release
    run_cmd(f"efs destroy release starburst {project} {release}")

    # Step 3: Check for remaining releases
    remaining_releases = list_releases(project)
    if remaining_releases:
        print(f"\n[INFO] Project '{project}' still has other releases: {', '.join(remaining_releases)}")
        print(f"Skipping project deletion.")
    else:
        # Step 4: Destroy project
        run_cmd(f"efs destroy project starburst {project}")
        print(f"\n[SUCCESS] Project '{project}' deleted since no other releases exist.")

if __name__ == "__main__":
    main()
