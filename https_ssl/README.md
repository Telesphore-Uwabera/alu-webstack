# Subdomain Information and HAProxy Configuration Project

This project consists of a Bash script for retrieving information about subdomains and a configuration file for HAProxy, a popular load balancer and proxy server. The Bash script allows you to display information about specific subdomains, such as their record type and destination IP address. The HAProxy configuration file defines how the proxy server should handle incoming requests and distribute them to backend servers.

## Subdomain Information Script

### Usage

To use the Subdomain Information Script, follow these steps:

1. Make sure you have Bash installed on your system.
2. Provide execution permission to the script by running the following command:

   ```bash
   chmod +x subdomain_info.sh
   ```

3. Run the script with a domain name as an argument:

   ```bash
   ./subdomain_info.sh example.com
   ```

   This will display information about the subdomains "www," "lb-01," "web-01," and "web-02" of the specified domain.

Alternatively, you can specify a subdomain as the second argument to get information about a specific subdomain:

```bash
./subdomain_info.sh example.com web-01
```

### Example Output

Here is an example of the output you can expect from the script:

```
The subdomain www is an A record and points to 192.168.1.1
The subdomain lb-01 is a CNAME record and points to load-balancer.example.com
The subdomain web-01 is an A record and points to 203.0.113.1
The subdomain web-02 is an A record and points to 203.0.113.2
```

## HAProxy Configuration

The provided HAProxy configuration file is set up to handle incoming HTTP requests and distribute them to two backend servers. It includes SSL/TLS termination, request redirection, and load balancing.

### Frontend Configuration

- The frontend "http-in" listens on port 80 and 443 with SSL termination.
- The "https_frontend" also listens on port 443 with SSL termination.
- Both frontends use the same SSL certificate located at `/etc/letsencrypt/live/www.randomall.tech/fullchain.pem`.

### Backend Configuration

- The "webservers" backend uses round-robin load balancing to distribute traffic between two backend servers: web-01 and web-02.
- Each backend server is specified with its IP address and port.

### Logging and Error Handling

- HAProxy logs are directed to `/dev/log` with local0 and local1 facilities.
- The configuration includes error files for various HTTP error codes to provide custom error messages.

### SSL/TLS Configuration

- SSL/TLS settings are configured with recommended ciphers and options for security.
- SSL certificates are expected to be located under `/etc/ssl/certs` and `/etc/ssl/private`.

## Contributors

- Telesphore Uwabera

## License

This project is licensed under the [MIT License](LICENSE.md).

## Acknowledgments

- Special thanks to the HAProxy community for their excellent documentation and support.
- [Let's Encrypt](https://letsencrypt.org/) for providing free SSL/TLS certificates.
