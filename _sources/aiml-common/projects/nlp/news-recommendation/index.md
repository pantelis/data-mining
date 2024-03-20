# News Time Machine

```{eval-rst}
.. youtube:: wArETCVkS4g
```

In this project you will be working to develop an **Django Ninja** based web app that implements a recommendation system. The web app will: 

1. Accept in a search text field, a query in natural language about a topic associated with `news`. 

2. Respond with an ordered table of all recommended to watch video clips across the **video vault** of a media outlet. The user will be able to select the order of the recommendations based on the following criteria: 

   - Most recent
   - Most relevant
   - Most popular
   

## Milestone 1: Django site

Learn one of the most popular web frameworks in the world, Django. You can start with the [official tutorial](https://docs.djangoproject.com/en/5.0/intro/tutorial01/) but bear in mind that you will also need to consult [Django Ninja](https://django-ninja.dev/) as **this will be the framework that you will use to build the API/App**.

You deliver a new repo (separate from your assignments repo) called `ninja-news` containing the docker compose based deployment of django ninja with postgres, redis, celery and Jetstream. You can borrow the structure of the project from [here](https://github.com/nickjj/docker-django-example) and ensure that the project is using Django Ninja. Your Django views in this app are based on [Bootstrap 5-based Tabler.io](https://tabler.io/preview) components. 

```{note}
Any dynamic UI interaction, if needed, must be based on [HTMX](https://htmx.org/) - eg [this guide](https://github.com/spookylukey/django-htmx-patterns).  
```

## Milestone 2: Data Model

Build a data model that will satisfy the needs of the project by making use of Pydantic 2 based data modeling tooling of Django Ninja. You can consult a slightly relevant to this exercise  [implementation](https://realpython.com/build-a-content-aggregator-python/) or any other implementation you think its relevant.  Note that the data model is for podcasts and you need to implement a quite different data model than this. 

Deliver the data model and a screenshot of the admin interface of the django site and as a screenshot of [DBeaver CE](https://dbeaver.com/docs/dbeaver/Database-Structure-Diagrams/) entity relationship diagram. Note that the initial data model will evolve over time as you will be adding more features to the app.

## Milestone 3: YouTube News Mining  

Using the Jetstream instance define a stream called "youtube-news" that publishes video content and content metadata in a stream. 

Using [this channel](https://www.youtube.com/channel/UCYfdidRxbB8Qhf0Nx7ioOYw) downloads the transcripts of the first (as ranked by youtube) K=10 videos from all 9 categories that youtube categorizes their news content (Top stories, Sports, Entertainment, Science, Health, Business, Technology, National, and World). Do not download `Live now` or `Upcoming` videos.

You may use the [youtube data api](https://developers.google.com/youtube/v3/docs) to retrieve the videos.

Each message of the jetstream will be serialized using [protobuf](https://protobuf.dev/getting-started/pythontutorial/) and will contain the following fields:

- `video_url`: The URL of the video
- `transcript`: The transcript of the video
- `channel`: The channel of the video
- `publication_date`: The publication date of the video
- `category`: The category of the video

The stream consumer(s) retrieve the messages and store them in the database table, exposing them to django apps via your data model. Ensure that only updates are stored and not duplicates.

Use the suggested template [tabler.io](https://tabler.io/preview) to produce the table on a view using the `Datatable` component visibnle in the route `/latest`. 

```{note}
If you want to deep dive deeper into the architectural patterns of an event based architecture specifically for the Python language you can consult [this chapter](https://learning.oreilly.com/library/view/architecture-patterns-with/9781492052197/ch08.html#idm45846301991608)
```

## Milestone 4: API

At this point you may want to switch off the publisher and the consumer of the jetstream and start working on the API. The reason is that you may hit Youtube quotas and blocked from downloading other videos. The professional way to do this is via [feature flags](https://waffle.readthedocs.io/en/stable/) but this is optional. 

The API must support the following external endpoints:

/summarize
/search

and other internal REST endpoints of your choice based on the needs of the app. 

The summarize endpoint uses existing OpenAI APIs to summarise the text of the transcript and is constantly running but invokes the OpenAI APIs only if new summaries are needed.  Periodic invocation may be achieved with [Celery](https://docs.celeryq.dev/en/stable/userguide/periodic-tasks.html).  

The view that supports this functionality is the original table with a new column called `summary` and the value points to a new view that presents two text fields: the left is the original transcript and the right is its summary. You can use [langchain](https://python.langchain.com/docs/get_started) to provide the summary and the invocation of the OpenAI API. 

The /search endpoint uses the LLM to recommend the most relevant videos based on the search query.

https://python.langchain.com/docs/expression_language/cookbook/retrieval

To be completed






