# C++, GitHub Actions, and Docker Test
This repo provides an example of building C++ projects using CMake and Ninja with GitHub Actions. Currently, Linux and Windows are supported, with Debug and Release builds for both.

## Tech
This demo uses a number of free and open-source projects to work properly:

- [GCC] - Cross platform C/C++ compiler
- [Visual C++ 2022] - C++ compiler for Windows from Microsoft
- [CMake] - Industry standard build system generator
- [Ninja] - Small build system focused on speed
- [Git] - Distributed version control system
- [GitHub Actions] - Automation for GitHub
- [Docker] - Container software
- [Chocolatey] - The package manager for Windows

## Building locally in Linux with Docker
> [!NOTE]
> These steps describes building the project with the generated directory within the top-level repo directory. See the commands in `build.yaml` for moving the generated directory outside of the top-level repo directory and verifying the build is 100% out-of-source.
1. Create the Docker image
   ```
   docker build -t <IMAGE_NAME>:latest .github
   ```
   **Example**
   ```
   docker build -t builder:latest .github
   ```
2. Build the project
    ```
    docker run \
      --rm \
      --name <CONTAINER_NAME> \
      --mount type=bind,source="$(pwd)",target=/Repo \
      --workdir=/Repo \
      <IMAGE_NAME>:latest \
      ./build_all <BUILD_TYPE>
    ```
    **Description**
    * `--rm` - Delete the container when it stops
    * `--name <CONTAINER_NAME>` - Desired name for the container
    * `--mount type=bind,source="$(pwd)",target=/Repo` - Mount the current directory in the container at `/Repo`
    * `--workdir=/Repo` - Working directory for the container
    * `<IMAGE_NAME>:latest` - Image to use for the container
    * `./build_all <BUILD_TYPE>` - Command to execute in the container

    **Example**
    ```
    docker run \
      --rm \
      --name builder \
      --mount type=bind,source="$(pwd)",target=/Repo \
      --workdir=/Repo \
      builder:latest \
      ./build_all Release
    ```

## Notes
* When reproducing this repository, ensure the `build_all` (and any other directly executed scripts) are added to **Git** with execute permissions.
  * Query permissions
    ```
    git ls-files --stage
    ```
  * Add execute permissions
    ```
    git update-index --chmod=+x <SCRIPT_FILE>
    git add <SCRIPT_FILE>
    ```

## Useful commands
### Remove all Docker data
> [!WARNING]
> This command will remove all Docker data, including images, containers, and network
  ```
  docker system prune -a
  ```

## License
GPLv3

   [GCC]: <https://gcc.gnu.org>
   [Visual C++ 2022]: <https://visualstudio.microsoft.com>
   [CMake]: <https://cmake.org>
   [Ninja]: <https://ninja-build.org>
   [Git]: <https://git-scm.com>
   [GitHub Actions]: <https://github.com/features/actions>
   [Docker]: <https://www.docker.com>
   [Chocolatey]: <https://chocolatey.org>