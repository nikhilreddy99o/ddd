#!/usr/bin/env python3

import os

def run_cmd(cmd):
    """Run and print a shell command."""
    print(f"\n> {cmd}")
    os.system(cmd)

def show_projects():
    """Display all existing projects."""
    print("\nAvailable Projects:")
    run_cmd("efs display metaproj starburst")

def show_releases(project):
    """Display all releases under a project."""
    print(f"\nReleases under project '{project}':")
    run_cmd(f"efs display project starburst {project}")

def delete_release_and_project():
    print("\n=== EFS Project & Release Deletion ===")

    show_projects()
    project = input("\nEnter the project you want to delete (e.g., trinob): ").strip()

    show_releases(project)
    release = input(f"\nEnter the release version to delete from '{project}' (e.g., 42): ").strip()

    print("\n[WARNING] This will DELETE release and project permanently from EFS.")
    print(f"You are deleting project: {project}, release: {release}")
    confirm = input("Type 'DELETE' to confirm: ").strip()
    if confirm != "DELETE":
        print("Aborted.")
        return

    # Step-by-step removal
    run_cmd(f"efs deprecate release starburst {project} {release} --type release")
    run_cmd(f"efs purge release starburst {project} {release}")
    run_cmd(f"efs destroy release starburst {project} {release}")
    run_cmd(f"efs destroy project starburst {project}")

    print("\n=== SUCCESS ===")
    print(f"Deleted release '{release}' and project '{project}'.")

if __name__ == "__main__":
    delete_release_and_project()
