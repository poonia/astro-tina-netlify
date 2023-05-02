---
title: Purpose of AEM Clientlibs
description: 'Different usages of AEM clientlibs '
pubDate: '2022-07-08T04:00:00.000Z'
heroImage: /placeholder-hero.jpg
---


AEM client libraries are a way of bundling CSS and JavaScript resources that are used in AEM web applications. Client libraries allow developers to organize their code into logical groups and make it easier to manage dependencies and update resources.

To use client libraries in AEM, you need to follow these steps:

1. Define a client library: You can define a client library by creating a node in the AEM repository under /apps or /etc, depending on whether it is a project-specific library or a shared library. The node should have a specific set of properties that define the resources included in the library, the categories, and other attributes.
2. Add resources to the client library: Once the client library node is created, you can add CSS and JavaScript files to it. The resources can be located in the file system or in the AEM DAM, and you can specify the location using the resource type, path, and category.
3. Include the client library in your component or template: You can include the client library in your component or template by referencing the client library node using a cq:includeClientLib tag. This tag will include the client library's resources in the HTML page when the component or template is rendered.
4. Load the client library on the page: Finally, you need to load the client library on the page by calling the client library manager's getClientLibrary() method. This method will generate the HTML code required to include the client library's resources on the page.

By following these steps, you can leverage AEM client libraries to organize your web application's resources and make it easier to manage and update them.
