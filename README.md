# Cloudflare Data Fabric

**Cloudflare Data Fabric** is an open-source framework designed to help teams build scalable data solutions, such as data lakes, data lakehouses, and data meshes, using Cloudflare’s suite of products. This framework offers a data fabric approach that combines storage, compute, and security to create a seamless data layer accessible across distributed environments.

## Key Features

- **Centralized Data Storage**: Utilizes [Cloudflare R2](https://www.cloudflare.com/products/r2/) as the primary storage layer for data objects, offering cost-effective, serverless data storage.
- **Serverless Data Processing**: Enables real-time data transformations and processing using [Cloudflare Workers](https://developers.cloudflare.com/workers/).
- **Traditional ETL Workflows**: Supports traditional, long-running ETL tasks through GitHub Actions with a self-hosted runner on Hetzner servers, providing powerful compute resources for data extraction, transformation, and loading at a low cost.
- **Authentication & Authorization**: Implements fine-grained access control with [Cloudflare Access](https://www.cloudflare.com/products/zero-trust/) for secure data access and policy enforcement.
- **Edge Caching and Optimization**: Leverages Cloudflare’s global CDN and edge network for efficient data delivery.
- **Multi-Purpose Data Buckets**: Provides separate public and private buckets for open and restricted data access, with role-based permissions.

## Use Cases

- **Data Lakes and Lakehouses**: Store raw and processed data for analysis, training, and model serving.
- **Data Mesh Architecture**: Decentralize data storage across domains with independent data governance.
- **Real-time Data Transformation**: Process and transform data on the fly as it’s accessed.

## Getting Started

### Prerequisites

To use Cloudflare Data Fabric, ensure you have:
- A [Cloudflare account](https://dash.cloudflare.com/sign-up) with access to R2 and Workers.
- Git installed locally for cloning and managing the repository.
- Node.js installed (for running the setup script).

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/cloudflare-data-fabric.git
   cd cloudflare-data-fabric
   ```

2. **Configure Cloudflare Services**:
   - Set up Cloudflare R2 buckets (public and private) in your Cloudflare account.
   - Enable Cloudflare Workers for your account.

3. **Install Dependencies**:
   Run the following command to install required dependencies:
   ```bash
   npm install
   ```

4. **Configure Environment Variables**:
   Create a `.env` file with your Cloudflare account details:
   ```env
   CLOUDFLARE_ACCOUNT_ID=your_account_id
   CLOUDFLARE_API_TOKEN=your_api_token
   ```

### ETL Process with GitHub Actions and Hetzner

For traditional ETL tasks, we use GitHub Actions with a self-hosted runner on Hetzner servers, providing powerful resources at an affordable cost. Here’s how to set this up:

1. **Set Up Hetzner Runner**:
   - Deploy a virtual server on Hetzner with sufficient CPU, memory, and storage for ETL workloads.
   - Install the GitHub Actions runner on your Hetzner server by following [GitHub’s self-hosted runner setup](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners).

2. **Runner Configuration**:
   - Configure your runner to scale according to ETL job requirements, allowing for efficient resource usage.
   - Use environment variables or secrets to securely manage credentials for data sources and destinations.

3. **ETL Workflow**:
   - Define ETL workflows using GitHub Actions. Schedule them with cron syntax for regular, automated runs:
     ```yaml
     on:
       schedule:
         - cron: '0 0 * * *' # Run daily at midnight
     ```
   - Use GitHub’s workflow visualization to monitor each run and set up notifications for errors or job completions.

4. **Data Access and Security**:
   - Securely access data sources from the runner, potentially using VPN or SSH tunneling if needed.
   - Store all sensitive information (API keys, credentials) in GitHub secrets for secure access during workflows.

### Example Code

```javascript
// Example: Access a file in the public R2 bucket
const fetchData = async () => {
  const response = await fetch("https://data-cloudflare.example.com/myfile.csv");
  const data = await response.text();
  console.log(data);
};
fetchData();
```

## Contributing

We welcome contributions! Please check the [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to contribute to the Cloudflare Data Fabric project.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
