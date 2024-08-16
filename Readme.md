# Debug Nodejs Bin Change

## Works with 20.15.1

Install global puts bin as described in the `package.json` into the global `bin` dir in the system, then is able to execute the command.

```
npm pack &&
  docker rm -f node &&
  docker run -dt --rm --name node node:20.15.1 /bin/bash &&
  docker cp debug-bin-1.0.0.tgz node:/root/debug-bin-1.0.0.tgz &&
  docker exec node npm install -g /root/debug-bin-1.0.0.tgz &&
  docker exec node debug-bin
```

## Doesn't work with 20.16.0

Install global doesn't put the bin as described in the `package.json` into the global `bin` dir in the system, then is unable to execute the command.

This is due to the file being in the hidden folder `.build`, if it is in a regular folder e.g. `build` it will work.

This also happens for packages installed from npm, just chosen here for reproducibility to pack locally, then install from tarball.


```
npm pack &&
  docker rm -f node &&
  docker run -dt --rm --name node node:20.16.0 /bin/bash &&
  docker cp debug-bin-1.0.0.tgz node:/root/debug-bin-1.0.0.tgz &&
  docker exec node npm install -g /root/debug-bin-1.0.0.tgz &&
  docker exec node debug-bin
```