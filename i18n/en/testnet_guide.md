# Getting started with the Kovri testnet

## Preamble

Kovri's testnet currently resides within a series of Docker containers and images which all communicating over a single Docker network.
This allows for private network testing and monitoring without the need to connect to the public kovri network.

## Prerequisites

- Linux development environment (Linux is currently supported)
   - See the kovri [README](https://github.com/monero-project/kovri#building) for a list of build dependencies
- [Docker](https://www.docker.com/)
   - The build user must have permissions to use Docker (added to the docker group, for example)
- A cloned repository
```bash
$ git clone --recursive https://github.com/monero-project/kovri
```

## Step 1: Create the testnet

For a complete list of options, run the `help` option:
```bash
$ ./kovri/contrib/testnet/testnet.sh help
```
You can export the listed environment variables from your shell or set them manually during setup.

Create the environment and set the values accordingly:
```bash
$ ./kovri/contrib/testnet/testnet.sh create
```
- For new developers, it is advised to use the defaults with the exception of your repository location
- See the Dockerfiles directory for available Dockerfiles to build during setup
- To keep the Kovri repo clean, choose a directory outside the repo

## Step 2: Running the Kovri testnet

Now that the testnet has been created, let's get it running.

1. Navigate to the Kovri repo
   * Ex: `cd /home/testuser/kovri`
2. Run the startup script
   * Ex: `./contrib/testnet/testnet.sh start`
3. All the testnet components will startup
4. Cat individual instance log pipes for a view of their logs:
   * Ex: `cat /home/testuser/testnet/kovri_010/log_pipe`
5. If monitoring is enabled, navigate to the Grafana endpoint in a browser:
   * Ex: `http://127.0.0.1:3030` with credentials `admin:kovri`
   * Click the `Home` icon to get a list of Dashboards
     * Details Containers: detailed statistics about container resource usage
     * Details NetDB: detailed statistics about Kovri instances' NetDB
     * Instance Overview: overall statistics of the Kovri tesnet environment
   * Each Dashboard can be filtered to show a subset of Kovri instances

## Step 3: Stopping the Kovri testnet

When the current round of testing is done, it's time to stop the testnet.

1. Navigate to the Kovri repo
   * Ex: `cd /home/testuser/kovri`
2. Run the shutdown script
   * Ex: `./contrib/testnet/testnet.sh stop`
3. You will be prompted to set a timeout interval
   * This is useful for allowing participating tunnels extra time to close
4. All of the Docker containers and network will begin shutting down

## Destroying the Kovri testnet

After all testing is done for this Kovri build, it's time to destroy the testnet.

1. Navigate to the Kovri repo
   * Ex: `cd /home/testuser/kovri`
2. Run the destruction script
   * Ex: `./contrib/testnet/testnet.sh destroy`
3. You will be prompted for a testnet working directory to destroy
   * Ex: `/home/testuser/testnet`
4. All of the Docker containers and network will begin shutting down
5. All of the Docker containers will be removed
6. You will be prompted for a Kovri testnet network to destroy
   * `kovri-testnet` is the default testnet network

## Running custom commands on the Kovri testnet

Sometimes, it may be useful to run a specific command within a Kovri Docker container.

Luckily, there's an option for that.

1. Navigate to the Kovri repo
   * Ex: `cd /home/testuser/kovri`
2. Run the execution script
   * For instance, let's say you need a bash shell
   * Ex: `./contrib/testnet/testnet.sh exec "bash"`
   * Other possibilities exist, and are left as an exploration for the reader
3. The Kovri repo is loaded into the temporary container, so one also has access to the Kovri binaries
   * Ex: From within the container: `./build/kovri` and `./build/kovri-util`
   * Note: It may be necessary to enter a bash shell, and rebuild the binaries