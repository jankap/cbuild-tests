
## Build

Building is a two-step approach.

1. First, generate `.cprj` files from `csolution.yml` files. They can be a) imported by µVision to build and debug and b) used to build the firmware via `cbuild` on command line.

    ```bash
    csolution convert -s ./prj/test.csolution.yml -o ./prj/generated-projects
    ```

2. Build
    * Use `cbuild` on commandline without debugging. Needs Linux in the remote/devcontainer:

        ```bash
        cbuild ./prj/generated-projects/test.release+HW_A/test.release+HW_A.cprj -i build-src/cbuild/tmp -o build-src/cbuild/test.release+HW_A
        cbuild ./prj/generated-projects/test.release+HW_B/test.release+HW_B.cprj -i build-src/cbuild/tmp -o build-src/cbuild/test.release+HW_B
        cbuild ./prj/generated-projects/test.debug+HW_A/test.debug+HW_A.cprj -i build-src/cbuild/tmp -o build-src/cbuild/test.debug+HW_A
        cbuild ./prj/generated-projects/test.debug+HW_B/test.debug+HW_B.cprj -i build-src/cbuild/tmp -o build-src/cbuild/test.debug+HW_B
        ```
