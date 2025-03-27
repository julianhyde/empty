# Empty HOWTO

Here's some miscellaneous documentation about using and developing Empty.

# Release

Make sure that `./mvnw clean install site` runs on JDK 8, 11 and 17
on Linux, macOS and Windows.
Also check [Travis CI](https://travis-ci.org/julianhyde/empty).

Upgrade dependencies to their latest release: run
```bash
./mvnw versions:update-properties
```
and commit the modified `pom.xml`.

Write release notes. Run the
[relNotes](https://github.com/julianhyde/share/blob/master/tools/relNotes)
script and append the output to [HISTORY.md](HISTORY.md).

Update the version number at the bottom of [README](README.md),
and the copyright date in [NOTICE](NOTICE).

Switch to JDK 21.

Check that the sandbox is clean:

```bash
git clean -nx
mvn clean
```

Prepare:

```bash
export GPG_TTY=$(tty)
mvn -Prelease -DreleaseVersion=x.y.0 -DdevelopmentVersion=x.(y+1).0-SNAPSHOT release:prepare
```

Perform:

```bash
mvn -Prelease -DskipTests release:perform
```

Stage the release:
* Go to https://oss.sonatype.org and log in.
* Under "Build Promotion", click on "Staging Repositories".
* Select the line "empty-nnnn", and click "Close". You might need to
  click "Refresh" a couple of times before it closes.

After testing, publish the release:
* Go to https://oss.sonatype.org and log in.
* Under "Build Promotion", click on "Staging Repositories".
* Select the line "empty-nnnn", and click "Release".

Update the [github release list](https://github.com/hydromatic/morel/releases).

Wait a couple of hours for the artifacts to appear on Maven central,
and [announce the release](https://x.com/julianhyde/status/622842100736856064).
