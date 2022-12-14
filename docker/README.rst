********************************************************************************
Docker images
********************************************************************************

This directory includes docker files to for Docker images.

Build Docker images for tests
======================================================================

See test-base directory if running without proxy.
See test-proxy directory if running with proxy.

Testing Code
======================================================================

Before running a container
----------------------------------------------------------------------

Set the Snowflake connection info in ``parameters.json`` and place it in ``pdo_snowflake`` directory:

.. code-block:: json

    {
        "testconnection": {
            "SNOWFLAKE_TEST_USER":      "<your_user>",
            "SNOWFLAKE_TEST_PASSWORD":  "<your_password>",
            "SNOWFLAKE_TEST_ACCOUNT":   "<your_account>",
            "SNOWFLAKE_TEST_WAREHOUSE": "<your_warehouse>",
            "SNOWFLAKE_TEST_DATABASE":  "<your_database>",
            "SNOWFLAKE_TEST_SCHEMA":    "<your_schema>",
            "SNOWFLAKE_TEST_ROLE":      "<your_role>"
        }
    }

Run Tests on Containers without proxy
----------------------------------------------------------------------

Mount ``/cfg`` and ``/base`` and start a container:

.. code-block:: bash

    cd pdo_snowflake
    docker run -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake:php7.0-ubuntu14.04 /base/docker/scripts/build_run_ubuntu.sh
    docker run -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake:php7.1-ubuntu14.04 /base/docker/scripts/build_run_ubuntu.sh
    docker run -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake:php7.1-ubuntu16.04 /base/docker/scripts/build_run_ubuntu.sh
    docker run -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake:php7.2-ubuntu18.04 /base/docker/scripts/build_run_ubuntu.sh

Run Tests on Containers with proxy
----------------------------------------------------------------------

Mount ``/cfg`` and ``/base`` and start a container:

.. code-block:: bash

    cd pdo_snowflake
    docker run --net proxytest --privileged -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake-w-proxy:php7.2-ubuntu14.04 /base/docker/scripts/build_run_ubuntu_with_proxy.sh
    docker run --net proxytest --privileged -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake-w-proxy:php7.2-ubuntu16.04 /base/docker/scripts/build_run_ubuntu_with_proxy.sh
    docker run --net proxytest --privileged -v $(pwd):/cfg -v $(pwd):/base -it pdo-snowflake-w-proxy:php7.2-ubuntu18.04 /base/docker/scripts/build_run_ubuntu_with_proxy.sh
