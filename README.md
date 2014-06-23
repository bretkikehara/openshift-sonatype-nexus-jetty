Openshift Sonatype Nexus DIY Cartridge
-------------------------

This [Openshift](https://www.openshift.com/) cartridge facilitates running a lightweight cartridge by storing only the [Sonatype Nexus](http://www.sonatype.org/nexus/) configurations. The build hook will download and configure the Sonatype Nexus Jetty bundle.

## Quickstart: Deploy from GitHub

1. Under the Openshift Applications tab, click `Create your first application now` link or the `Add Application` button.
2. Create a `Do-It-Yourself 0.1` application.
3. After selecting your public URL, paste the GitHub **HTTP** repository clone URL. (Just remove the `S` from the HTTPS repository clone URL)

	http://github.com/bretkikehara/openshift-sonatype-nexus-jetty

4. Wait a few minutes while the application is built.
5. Login to the Sonatype Nexus application using the default user `admin` and password `admin123`.

## Sonatype Nexus

[Sonatype Nexus](http://www.sonatype.org/nexus/) serves as a Maven repository.

Current Deploy Version: ***2.8.1-01*** community edition

The deploy version can be changed by setting the version in the `.openshift/action_hooks/build` script.

## Openshift

All hooks are available under the `.openshift/action_hooks` directory.

### Build Hook
Currently, the build hook downloads the the Nexus bundle and then proceeds to deploy it to `$OPENSHIFT_DATA_DIR`. This can be changed by updating the `NEXUS_VERSION` in the `.openshift/action_hooks/build` script. ***NOTICE: Any existing version of the nexus deployment will be deleted!***

If `sonatype-work` directory does not exists, then a copy is made in the `$OPENSHIFT_DATA_DIR`. Otherwise, this folder will not be touched across deployments.

### Start Hook

The following environment variables are set in the start hook:

	NEXUS_APPLICATION_PORT
    NEXUS_APPLICATION_HOST
    NEXUS_CONTEXT_PATH
    NEXUS_WORK
    NEXUS_HOME

When running the Sonatype Nexus application, anything that is printed to the System.out is captured in the `$OPENSHIFT_DIY_LOG_DIR/out.log` file.

### Stop Hook

Runs the kill command to stop the server.

## License

This project is available under the MIT License.