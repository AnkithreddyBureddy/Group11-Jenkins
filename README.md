# Group11-Jenkins

Edited this file to trigger pipeline automatically


# HTML Application Deployment

This project is a simple HTML application, which includes a basic webpage with an `index.html` file and other supporting files like `Jenkinsfile` and `README.md`.

## Project Overview

This project is set up with Jenkins for continuous integration and continuous deployment (CI/CD). The following stages are involved:

1. **Checkout**: The project code is fetched from GitHub.
2. **Setup**: Creates a `build` directory to house all the necessary files for deployment.
3. **Build**: Copies the necessary files from the project directory to the `build` directory.
4. **Test**: Ensures that the `index.html` file exists and is valid.
5. **Deploy**: The build is deployed to the target server or directory.


## Technologies Used

- **HTML**: For the structure of the application.
- **Jenkins**: For automating the CI/CD pipeline.
- **GitHub**: Source code repository.
- **Ngrok**: Exposes Jenkins to the public for webhooks.
  
## Setup

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/AnkithreddyBureddy/Group11-Jenkins.git
![Uploading image.png…]()
