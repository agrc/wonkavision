# wonkavision

A CLI tool to make deploying things over SFTP simple.

![tophat](https://user-images.githubusercontent.com/325813/91506198-c8cb7b00-e88e-11ea-9215-bad08585248a.png)

## Getting Started

1. `npm install @agrc/wonkavision`
1. Create `.env` file in the root of your project and populate with these values:

    ```text
    SSH_HOST=...
    SSH_USERNAME=...
    SSH_PASSWORD=...
    ```

1. Add a new npm script to your `package.json` file:

    ```json
    "scripts": {
      "deploy": "wonkavision clean && npm run build && wonkavision zip && wonkavision ship ./deploy/deploy.zip destination && wonkavision unzip destination"
    }
    ```

## Commands

- `clean`: Folder locations to clean
  - `artifacts`: Array of string paths relative to the package.json
    - The no argument default will remove the `./deploy` directory
- `zip`: Compress files into one location
  - `src`: The source folder to compress
    - The no argument default is `./build`
  - `dest`: The file path to place the compressed files
    - The no argument default is `./deploy`
  - `name`: The name of the zip file
    - The no argument default is `deploy.zip`
- `ship`: Sends the zip file to the destination
  - `src`: The parent folder or file to ship
    - The no argument default is `./deploy/deploy.zip`
  - `dest`: The folder to place the zip file
    - The no argument default is `app`
- `unzip`: Decompress files on the SSH host, deleting the zip file after decompression
  - `dest`: The destination folder containing the zip file
    - The no argument default is `app`
  - `name`: The name of the compressed zip file
    - The no argument default is `deploy.zip`
  - `--extra-command`: a command to run after the zip file is decompressed

_All commands can be run with a `--dry-run` flag to not perform any action`_
