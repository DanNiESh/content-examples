# README for All-Tests.ipynb

## Introduction

- The purpose of these tests is to verify compatability for new projects, which can vary between professors, users, and courses
- Tests can be expanded upon to suit the needs of users and books

## Customization

- To customize, create a new cell inside `All-Tests.ipynb`
  - If test fails, append the string `"Test Name" Failed` to ERRORS array with the name of the error, otherwise, pass the string to PASSES array
  - Example template:

    ```python
    # Define the test and conditions

    test_command = "<INSERT TEST COMMAND HERE>"
    expected_result = "<INSERT EXPECTED RESULT HERE>"
    environment_variables = "<INSERT REQUIRED VARIABLES IF APPLICABLE>"

    def perform_test(command, expected_result):

        execution_result, output = shelltest(command)

        if output == expected_result:
            # If test passes, add to the PASSES array 
            PASSES.append("<TEST NAME> PASSED")
        else:
            # If test fails, add to the ERRORS array with error message
            ERRORS.append("<TEST NAME> FAILED: " + output)

    # Run test to verify success
    perform_test(test_command, expected_result)
    ```

## Test Descriptions

### Write Permission to Home Directory Test
- Confirms that the notebook user has permission to write, read, and execute files within their `/home` directory

### Environmental Variables test
- Confirms that the environment variables set from `Dockerfile` still exist and maintain the same values within the Jupyter Notebook
- Ensures that the user has a valid UID and GID within a customizable range

### ASLR Test
- Runs gdb 100 times on date binary stopping at first instruction and grep ld. If ld is found at same address following command has a value of 1 then ASLR is properly disabled.
- We want to disable ASLR so that students can use GDB properly in their environments.

### Network Test
- Ensures that user can send and receive network packets from websites

### Pip-Conda Test
- Ensures that the user can install Python-based packages using `pip`

### Git and SSH Test
- Tests if Git and SSH configuration files are permanent and working

### Permissions Test
- Test if conda directories are read/writable

