## Purpose

Store shared (mustache) templates to be used by the implementation of `JavaScriptBuilderElement` and other components across the languages. 

## Background

The [language-independent specification](https://github.com/51Degrees/specifications) describes how JavaScriptBuilderElement is used [here](https://github.com/51Degrees/specifications/blob/36ff732360acb49221dc81237281264dac4eb897/pipeline-specification/pipeline-elements/javascript-builder.md). The mechanics is: javascript file is requested from the server (on-premise web integration) and is created from this mustache template by the JavaScriptBuilderElement. It then collects more evidence, sends it to the server and upon response calls a callback function providing the client with more precise device data.

## Cookies -> Session storage Transformation 

The processJsProperties function in javascript template has a section that uses regex to search the injected JavaScript for any commands that set cookie values to the browser's document object. It then transforms this command so that it sets session storage values instead. This format should be accounted for when writing JavaScript properties. 

## Shipping / Deployment

This repo is not a stand-alone package, but is shipped as part of and used by each of the following repositories / packages:
- [pipeline-dotnet](https://github.com/51Degrees/pipeline-dotnet) as a submodule
- [pipeline-java](https://github.com/51Degrees/pipeline-java) as a submodule
- [pipeline-node](https://github.com/51Degrees/pipeline-node) as a submodule
- [pipeline-python](https://github.com/51Degrees/pipeline-python) as a submodule
- [pipeline-php-core](https://github.com/51Degrees/pipeline-php-core) as a static dependency

Wherever it is a submodule it will be updated by `Nightly Submodule Update` action, wherever it is a static dependency it will be updated by the `Nightly Package Update` action within a target repository.

No special action is needed from the user to deploy the template, just be aware that any changes introduced in this repo will automatically propagate and affect the above packages. 
