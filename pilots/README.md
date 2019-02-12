# Pilot Packages

The pilot packages are the alpha tester of this working group. They will help us to archive our
[WG goals](https://github.com/nodejs/package-maintenance#goals):
+ identifing the major problems a module have to face
+ defining priorities for our todo-list
+ verifing the benefits of the tools and process built
+ improving all the stuff created to evangelize the community

The help provided to all these packages will be to think and to implement solutions for their problems,
as helping them to migrate to newer Node.js versions.

Doing so we will create a wide range of tools in order to:
+ give to all the maintainers the possibility to use them
+ provide the resources to choose wisely the dependencies for business
+ improve the quality and stability of the packages in the Node.js ecosystem


## List

| Package* | Maintainer Reference |
|----------|----------------------|
| [Express]     | [@wesleytodd](https://github.com/wesleytodd)
| [MQTT]        | [@mcollina](https://github.com/mcollina)

[Express]: https://github.com/expressjs/express
[MQTT]: https://github.com/mqttjs/MQTT.js

*Ordered per joining time.


## Approach

The baseline to start with this work is:

+ Prepare a [survey](./SURVEY.md) to collect more informations as possible
+ Think out the feedback received in tasks we should do to help the package
+ Brief with other pilot packages feedbacks to find common needs
+ Define a roadmap
+ Implement the roadmap
+ Coordinates with pilot packages to try the solutions implemented and verify the benefits
+ Share to the community the tools and the succesful process


## Output

During this phase of work, all the docs and useful stuff must be stored
in the directory `./pilots/${package-name}/`. This directory can be merged in master
whenever a main approach's step is reached.

We should produce almost:

| Docs | Description |
|------|-------------|
| SURVEY_ANSWER.md | Collect all the information received from the Maintainer Reference
| TASKS.md         | An initial list of tasks based on the survey's answers
| ROADMAP.md       | All the tasks that will be implemented (a list of issues links) with some target to aim
| RESULTS.md       | At the end of the pilot phase, we should recap what we learned about the package itself and how the know-how could be shared
