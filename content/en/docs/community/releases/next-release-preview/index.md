---
title: "Next Release Preview"
linkTitle: "Next Release Preview"
weight: 2
description:
---

Please make a pull request to describe any changes you wish to highlight
in the next release of Spinnaker. These notes will be prepended to the release
changelog.

## Coming Soon in Release 1.23

### (Breaking Change) Spinnaker Kubernetes manifest image overwriting with a bound artifact

Spinnaker will now overwrite images in a manifest with a bound artifact if the
input manifest's image has a tag on it. The previous behavior was that Spinnaker
would only overwrite images in a manifest if the image did not have a tag.

https://github.com/spinnaker/spinnaker/issues/5948

### Kubernetes accounts no longer use the liveManifestCalls flag

As of this release, Kubernetes accounts no longer read the value of the
`liveManifestCalls` flag. Instead of using this flag, Spinnaker now decides
whether to read from the cache or directly from the Kubernetes cluster based on
the context of the request.

From a practical perspective this means that:

- Users who had `liveManifestCalls` enabled will see the same fast deploys as
  always but will no longer experience
  [bugs with dynamic target selection](https://github.com/spinnaker/spinnaker/issues/5607).
- Users who had `liveManifestCalls` disabled will notice significantly faster
  deployments.

Users may wish to remove the `liveManifestCalls` flag from their account
configuration, though this is not required and any configured value for this
setting will be ignored by Spinnaker.

### Java 11 is Required

Spinnaker now requires a Java 11 (or greater) runtime:
- If you use the community Docker containers, these have been using Java 11 for several releases now. No changes are required.
- If you are using the community Debian packages, you need to make sure a Java 11 runtime is available on your system.
- If you're building your own Spinnaker binaries from source, you will need to use a Java 11 JDK.