# TLS Encryption Configuration Script

These scripts streamline the creation of TLS certificates to ensure the security of **Cassandra**, **ElasticSearch**, **OpenSearch**, **NATS**, or **DataMiner** instances. They automate the entire process, encompassing the generation of a Root Certificate Authority (CA) certificate, node-specific certificates, and seamless certificate management tasks.

## Prerequisites

- Ensure you have Administrator privileges to execute the scripts successfully.
- Ensure that the **openssl** and the **keytool** executables are available on your system.

> [!WARNING]
>
> We have noticed issues when using the keytool of a different Java version then the version used by Cassandra/Elastic/OpenSearch. For this reason we highly recommend to use the keytool executable of the Java installation used by Cassandra/Elastic/OpenSearch.

### Linux/Mac

#### OpenSSL

Linux should come with OpenSSL by default. You can verify this by running the following command:

```bash
openssl version
```

#### keytool

Keytool is automatically installed when installing Java, so it should be present on the system if you have Cassandra/ElasticSearch/OpenSearch installed.

### Windows

#### OpenSSL

We have noticed issues with installing OpenSsl on windows. We found it the easiest to install [Git](https://git-scm.com/downloads) which ships an openssl executable with it. The executable can be found at `%programfiles%\git\usr\bin\openssl.exe`

#### Keytool

Keytool is shipped alongside with Java. ElasticSearchg and Cassandra installations on Windows also ship Java alongside. You can find the keytool executable at: `%programfiles%\ElasticOrCassandra\java\bin\keytool.exe`

## Usage

### Running `generate-tls-certificates.sh` (Linux/Mac)

1. Open a terminal.
2. Navigate to the directory containing `generate-tls-certificates.sh`.
3. Run the following command:

    ```bash
    chmod +x generate-tls-certificates.sh
    ```

    This step ensures execution permissions.

4. Execute the script:

    ```bash
    ./generate-tls-certificates.sh
    ```

### Running `generate-tls-certificates.ps1` (Windows)

1. Open PowerShell as administrator.
2. Navigate to the directory containing `generate-tls-certificates.ps1`.
3. Execute the script:

    ```powershell
    .\generate-tls-certificates.ps1
    ```

> [!NOTE]
> Ensure the necessary executables and prerequisites are in place before running the scripts.

## Features

- **Organization Type:** Choose the instance type for which you want to generate certificates (Cassandra, Elastic, OpenSearch, NATS, DataMiner).
- **Cleanup:** Option to clean up files generated in previous executions.
- **Cluster Information:** Enter the name of your cluster and handle non-ASCII characters appropriately.
- **Certificate Options:** Set the validity period for the certificates.
- **Key Size:** Choose the certificate key size (1024, 2048, 4096, or 8192 bits).
- **Hostnames:** Input the hostnames (FQDN) of each node.
- **Automatic Hostname Resolution:** Option to resolve hostnames automatically instead of manually entering IP addresses.
- **Root CA Certificate:** Choose to use an existing root certificate or generate a new one.
- **Certificate Generation:** Automatically generates certificates for each node in the cluster.
- **Subject Alternative Names (SANs):** Specify additional SANs for each node.
- **Password Handling:** Option to generate or enter separate passwords for the root CA private key and the per-node keystore/PKCS#12 output.
- **PKCS#12 Output:** Produces a single final `*-node-keystore.p12` per node, suitable for node deployment and DataMiner HTTPS certificate usage.
- **Cleanup Unused Files:** Remove unnecessary files generated during the execution.
- **Certificates Information:** Display information about the generated certificates, keystore files, and passwords.

> [!IMPORTANT]
>
> - Ensure the root CA certificate (rootCA.crt) is trusted on every client. **If a password is generated, note it down for future reference.**
> - Copy the generated PKCS#12 files (`*-node-keystore.p12`) to their respective nodes or DataMiner servers.

## License

This script is provided under the [MIT License](https://github.com/SkylineCommunications/generate-tls-certificates/blob/main/LICENSE.md).
