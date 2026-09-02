# About this project

This project provides a set of tasks and scripts used to create and update images used by spread.

This documents explains the images matching criteria and shows the examples to add and update all the supported images.

# OpenStack Backend

The following sections explain the images matching criteria used on OpenStack and show how to create/update images used to run the snapd test suite.

## Base images

Base images are images with no extra dependencies or special configuration, just the settings needed to boot on OpenStack. Those images are used as a base to create final images with the test dependencies required by the snapd test suite.

Some base images are created as part of the snapd project, and others can be imported from external image sources when needed.

The criteria for naming base images on snapd-spread project follows the rule:

	name: <osname>-<version>-<arch>-base
	description: Base Image

To create a base image, use the tasks described in the following section "Add new images". To create a final image, use the tasks described in the following section "Update images".

## Add new images

For OpenStack, use the helper script in `lib/openstack.sh` instead of invoking Openstack tasks directly.

Command pattern:

    ./lib/openstack.sh add-image --backend <openstack|openstack-arm|openstack-stg|openstack-stg-arm> --task <task-name> --target-system <target-system> [--property key=value]

Example:

    ./lib/openstack.sh add-image --backend openstack --task ubuntu-26.10-64 --target-system ubuntu-26.10-64-base

## Update images

For OpenStack, use the helper script in `lib/openstack.sh` to update images from a base system.

Command pattern:

    ./lib/openstack.sh update-image --backend <openstack|openstack-arm|openstack-stg|openstack-stg-arm> --task <task-name> --source-system <source-system> --target-system <target-system> [--property key=value]

Example:

    ./lib/openstack.sh update-image --backend openstack --task ubuntu-26.04-64 --source-system ubuntu-26.04-64-base --target-system ubuntu-26.04-64

The update tasks are intended to update a base image installing test dependencies and updating and configuring the system to run the snapd test suite optimally. Some update tasks use base images which are generated on the snapd-spread project, and other take images from other projects such as we get ubuntu-1604-lts images from project ubuntu-os-cloud.

