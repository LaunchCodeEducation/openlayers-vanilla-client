# Migrating From Single-Host

In a multi-host architecture your client and API codebases are physically separated from each other both in development and deployment. Changes to the client codebase, which are the most frequent, do not require restarting, rebundling or redeploying the API. The architecture is referred to as multi-host because The client code is served on a static HTTP server and the API code is served from its own application server. Each of which run on their own unique process and port.

The advantage of this architecture is that the frontend, or view layer, is physically decoupled from the backend, or model and controller layers. This means that their only technical constraints are the upholding and usage of endpoints the API exposes to the client. This is the interface by which the two communicate. As long as the interface remains constant (paths, request and response bodies) don't change then the implementation details (internal code, technologies and design patterns) used in either side are able to be modified without affecting the other.

This modern architecture provides an empowering freedom for developers on either side to develop and deploy their code independently. Most importantly it means that development can be an agile process where solutions are developed and shipped as needed without relying on the release schedule of the other codebase(s). Teams can have distinct ownership and scope over their work which provides the narrowly defined environment needed to design and develop solutions at the speed of modern demand.

## Project Organization

The first step in migrating the codebase is to determine whether it is better to use one repo for each codebase or a single repo tracking the history of both. These two approaches are dubbed polyrepo and mono-repo respectively. Like all decisions in web development there are advantages and disadvantages for either choice. What is important is to consider the requirements and contexnt of the project and see which of the options fits best.

## PolyRepo vs MonoRepo

### MonoRepo Benefits

- a good fit for simpler projects with 2 components or a collection of small but tangentially related components
- simple migration only requiring changes to the organization of a project's file system
- simpler to keep track of with the single repository and shared commit history

### MonoRepo Disadvantages

- does not scale well for large teams and projects with many unrelated components
- potential for massive repos where release and communication channels are mixed and lost in the noise
- encourages developers to take shortcuts with tight coupling of shared modules across multiple components by using file system linking instead of externally sourced dependencies
- requires a strictly enforced branch, commit and tag pattern to maintain order in larger repos

### PolyRepo Benefits

### PolyRepo Disadvantages

# MonoRepo Migration

As discussed above the monorepo is certainly the simplest migration to make. This is the suggested approach for migrating your existing project. You can continue to use the same repo and will only need to make file system changes to reorganize and separate the project. The final file system will look like this:

```sh
repo-name/
  .git # <-- single git repository tracking history of both codebases
  start.script # <-- an optional script (in your chosen language) that starts up both servers during developent
  api/ # <-- all backend API code, build and configuration files
    .gitignore # <-- git ignoring rules respective for the API codebase
  client/ # <-- all frontend client code, build and configuration files
    .gitignore # <--- git ignoring rules for the client codebase
```

## Encapsulating the API

First you should create an `api` directory and move everything short of the `.git` directory into it. Don't forget to move other dot files like `.gitignore`.
