# Work with EdgeRoutine CLI

Alibaba Cloud Content Delivery Network \(CDN\) provides the EdgeRoutine CLI to run custom JavaScript code on CDN nodes. This topic describes how to use the EdgeRoutine CLI to deploy JavaScript code.

The runtime environment of the EdgeRoutine CLI must be Node.js 8.0 or later.

To enable EdgeRoutine, you must map the serverless computing environment on CDN nodes to your accelerated domain name. If you have not prepared the accelerated domain name and AccessKey information for mapping, you must log on to the Alibaba Cloud CDN console with your Alibaba Cloud account. In the console, you can add the domain name to Alibaba Cloud CDN. For more information, see [Add a domain name to Alibaba Cloud CDN](/intl.en-US/Quick Start/Add a domain name to Alibaba Cloud CDN.md). You can also view your AccessKey information including the AccessKey ID and AccessKey secret in the console. For more information, see [Create an AccessKey pair]().

1.  Install the EdgeRoutine CLI.

    Open your terminal and run the following command to install EdgeRoutine CLI:

    ```
    $ npm install @alicloud/edgeroutine-cli -g
    ```

    **Note:** The latest version of the EdgeRoutine CLI is 2.0.0. After the installation, you can run the `edgeroutine-cli -v` command to query the version number. We recommend that you upgrade your EdgeRoutine CLI to the latest version.

2.  Run the following command to create a code directory and change to the directory:

    ```
    $ mkdir yourProject; cd yourProject
    ```

3.  Initialize the environment and create a code template.

    Run the following command to initialize the environment:

    ```
    $ edgeroutine-cli init
    ```

    The following example shows a code template. If you want to use your own code, you can move your code file to the code directory that you have created, and rename the code file edge.js.

    ```
    /**
     * Add the necessary event listener
     * @param {Event} fetch event, {Function} async function
     */
    addEventListener('fetch', event => {
      event.respondWith(handleRequest(event.request))
    })
    /**
     * Make a response to client
     * @param {Request} request
     */
    async function handleRequest(request) {
      return new Response('Hello World!', { status: 200 })
    }
    ```

4.  Configure the accelerated domain name and the AccessKey pair, including the AccessKey ID and AccessKey secret.

    ```
    $ edgeroutine-cli config
    ```

5.  Deploy the code to the canary release environment.

    **Note:** Before you deploy the code to the production environment, you must validate the code in the canary release environment.

    1.  Build the code in the canary release environment.

        ```
        $ edgeroutine-cli build
        ```

    2.  View the code in the canary release environment.

        ```
        $ edgeroutine-cli build --show
        ```

    3.  Delete the code in the canary release environment.

        This operation deletes configurations from the canary release environment. Proceed with caution.

        ```
        $ edgeroutine-cli build --delete
        ```

6.  Validate the code in the canary release environment.

    You must connect to the accelerated domain name in the terminal environment by using the IP address of the canary environment for EdgeRoutine. The IP address is 42.123.119.50 or 42.123.119.51.

    ```
    $ curl-v'http://yourdomain.com/yourpath/'-x42.123.119.50:80
    ```

7.  Deploy the code to the production environment.

    1.  After you validate the code in the canary release environment, you can deploy the code to the production environment.

        ```
        $ edgeroutine-cli publish
        ```

        **Note:** EdgeScript and EdgeRoutine use the same deployment system. If you use [EdgeScript](/intl.en-US/EdgeScript/Introduction/Overview.md) and EdgeRoutine at the same time, the `edgeroutine-cli publish` command that is run in the EdgeRoutine CLI will deploy scripts of both EdgeScript and EdgeRoutine from the canary release environment to the production environment. Before you deploy code, you can run the `edgeroutine-cli build -s` command to query scripts of EdgeScript and EdgeRoutine that are in the canary release environment. After you confirm the configurations that you want to deploy to the production environment, run the edgeroutine-cli publish commend to deploy the configurations.

    2.  View the code in the production environment.

        ```
        $ edgeroutine-cli publish --show
        ```

    3.  Delete the code in the production environment. Then, the code and relevant configurations are deleted. This step is optional.

        ```
        $ edgeroutine-cli publish --delete
        ```

8.  Run tests in the production environment.

    You can test the workloads of the accelerated domain name in the production environment.

    ```
    $ curl -v 'https://yourdomain.com/yourpath/'
    ```


