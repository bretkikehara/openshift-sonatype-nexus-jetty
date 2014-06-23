Openshift Sonatype Nexus DIY Cartridge
-------------------------

This project facilitates a lightweight cartridge with the [Sonatype Nexus](http://www.sonatype.org/nexus/) configurations only. Since the build hook downloads and configures the Sonatype Nexus Jetty bundle, this code repository only stores the hooks and the custom Nexus configurations.

## Hooks

All hooks are available under the `.openshift/action_hooks` directory.

### Build
Currently, the build hook downloads the `2.8.1-01` version of the nexus repository and then proceeds to deployt it to `$OPENSHIFT_DATA_DIR`. This can be changed by updating the `NEXUS_VERSION` in the `.openshift/action_hooks/build` script.

If `sonatype-work` directory does not exists, then a copy is made in the `$OPENSHIFT_DATA_DIR`.

### Start

The following environment variables are set in the start hook:

	NEXUS_APPLICATION_PORT
    NEXUS_APPLICATION_HOST
    NEXUS_CONTEXT_PATH
    NEXUS_WORK
    NEXUS_HOME

When running the Sonatype Nexus application, anything that is printed to the System.out is captured in the `$OPENSHIFT_DIY_LOG_DIR/out.log` file.

### Stop

Runs the kill command to stop the server.