# Football Transfer Analyst - Project Plan

## Problem Statement
Transfers are a big talking point in football. In the modern era fans are often quick to jump on players and label them failures as soon as they can. Often this is because of a lack of goals or assists, football's main and easiest to understand metrics. But if you know football, you know goals and assists don't tell the full story.

Take **Florian Wirtz** for example.

At the time of writing this he has played 8 league games and has 0 goals or assists, leading to him being a target of significant slander from opposition fans as well as some from his own. The list of new signings in similar predicaments goes on.

But this raises the question:

_Are they actually playing bad?_

This project attempts to answer that question using statistics and machine learning - going beyond just goals and assists. With this project we'll be able to find out whether players have been playing well, playing badly or somewhere in between. Whether they've been lucky, unlucky or a bit of both. In the case of Florian Wirtz, when you look into the in-depth statistics you'll find that this supposed "flop" is in the upper echelons of shot creating actions, expected assists, progressive passes and successful dribbles of players in the Premier League. He's making things happen, but is that enough? As part of this project we want to give you the context to make your own judgements on how a player is performing, with the help of stats to help you make that decision.

We'll be looking into advanced metrics such as xG (expected goals), xA (expected assists), chances created, and many more to truly derive player performance. By training models to detect patterns in player contributions, we can evaluate their impact more objectively with ratings based on their current performance, as well as potential (predicted performance).

Ultimately, this project hopes to challenge the narrative around underperforming players and provide a data-driven lens through which fans, analysts, and clubs can assess transfer success more fairly. 

## Solution Overview
So how are we going to approach this problem?

I'm sure by now you would've used an LLM (Large Language Model) in the form of ChatGPT or something similar, but if you have you would've realised they're great at giving you information but sometimes lack the access to the tools they need to really solve your problems. That's where Agentic AI comes in. With AI agents we can give our LLMs access to tools of your choice, ranging from simple code functions all the way to access to web searches and API calls.

This topic feels like the perfect use case for Agentic AI, so we're going to get our hands dirty with that. We're going to give our agent/s access to the following tools for our project:

 - We need a tool that provides stats, we can do this through a tool that scrapes websites with statistical information. 
 - We then need a way to rate how a players been doing, let's do this with a machine learning model. 
 - We'll also incorporate web search tools in order to give the agent access to more information, mainly for historical research and comparison. 
 - After our agent gets to work, we need a place to store the data, hence we will be using a database.
 - Finally, we want a way for users to interact and utilise this product, hence we will be building a user interface. 
 
 With all these elements we should have a model that can help us understand if these players really are playing as bad (or good) as the media is saying.

## Components
### Scraper
The scraper is going to be necessary in order to get current and up-to-date statistics for the agents and machine learning models to use.
 - We'll be using Beautiful Soup for website scraping
 - Planning to scrape from FBref or Statsbomb as of 21/10

### Rating System
There are two aspects to the rating systems that we will be building.
 - A current rating based on their performances thus far
 - A predicted rating based on their current statistics, how "lucky" they've been and historically similar players 

The luck factor will be depicted by looking into expected assists vs actual assists in order to understand whether their teammates have been converting the chances they've been creating or not. 

We will be using an XGBoost machine learning model for the current rating, trained on FBRef statistical data with Sofascore ratings as targets. The predicted rating will require an AI agent to leverage the current rating and factor it against historical scenarios and luck factor to create a predicted rating (time frame to be decided).

### Agent

Initially we're planning on building a **single-agent workflow**. This singular agent will have access to the below tools and synthesise them:
 - Scrape statistical data (using Beautiful Soup)
 - Calculate current performance rating (ML model)
 - Compute luck rating (calculated from stats)
 - Researches context (web search tool)
 - Finds historical comparisons (web search tool)

After the single agent system is up and running we plan to evolve to a **multi-agent workflow** as follows:

**Multi-agent Workflow Plan**

1. **User Query**

    _The user initiates a request._

2. **Coordinator Agent** 
   
    _Orchestrates the workflow by delegating tasks to different agents._

3. **Specialised Agents** 


    
    - 📊**Stats Agent** → Fetches and analyzes stats
    - 📰**Context Agent** → Searches for injuries/news/tactics
    - 🎞️**Historical Agent** → Finds similar historical cases
    - ⚖️**Comparison Agent** → Compares with multiple players
    - 🔮**Prediction Agent** → Predicts future performance
    - 🤓**Synthesis Agent** → Combines everything into final report


4. **Final Answer**

    _The system returns a comprehensive response based on all the above data and information._


✅ **Benefits of Multi-Agent Design:**

 - Modularity: Easier to maintain and upgrade individual components.
 - Parallelism: Agents can work concurrently, improving efficiency.
 - Scalability: New agents can be added as needed without disrupting the system.

### Database

In order to store the data and information from searches for later use we need a database. Particularly in the case that a user requests a player that's already been researched, it's useful for us to have a database to reach into so we can optimise performance. 
We also need a database to train the machine learning model on, thus this is a necessity.

This file will be updated as the decision is made, but for now we're considering the following databases:
 - MySQL
 - SQLite
 - DuckDB

As of now (21/10) we are leaning towards DuckDB.

### User Interface
We want to incorporate a frontend into this project to make it user friendly. The way we want to do this is with a Streamlit UI.

This UI will allow a user to input a player of their choice and receive information such as:
 - Current rating
 - Predicted rating
 - Luck scores
 - Player comparisons 

Essentially this will give the user most of the information that the agents see in a well formatted way. 

Ideally we will also be able to extend the User Interface to including dashboards and graphics, however we want to get this up and running with a simple informational output first.


## Timeline

| Week | Task                     |
|------|---------------------------|
|  0  | Foundations  |
| 1 - 2 | Core Build  |
| 3  | Enhancements |
| 4  | Documentation and Completion  |


## Success Criteria

For this project to be considered complete, it needs to have met all the success criteria:
 - A working multi-agentic workflow with an orchestrator agent instructing other agents, each with access to their own tools.
 - A machine learning model that gives player ratings based on sofascore ratings to a strong (80% or higher) validation accuracy. 
 - A scraper that accurately scrapes all valuable statistical information as requested by the orchestrator agent
 - A database that can handle data for machine learning training, as well as gather data from previous uses
 - An interface that allows a user to input a player (new signing) that they're curious about, and that returns all the relevant information for them to understand statistically how the player has been performing and how they are expected to play
 - Dashboards and graphics featuring information about new signings in the home page

## Learning Objectives
 - **Agentic AI** - Develop an understanding of Agentic AI and how to utilise it
 - **Web Scraping** - Develop a practical understanding of Web Scraping tools
 - **Machine Learning** - Utilise my understanding of Machine Learning in a practical setting and experiment with XGBoost
 - **Database** - Build on my previous DuckDB practice and understand how to create and utilise the database
 - **UI** - Build on my previous Streamlit attempt to create a consumer friendly user interface for the project

## Risks & Mitigation

 - Data availability
    - Websites may block scraping
    - May change structure
 - Misinterpretation of statistics
    - Many of these statistics 

## Author Note

This project attempts to bring together most of the technologies I have worked on and experimented with this year. The topic, despite being niche, was chosen given it's something that I'm passionate in and thus well-versed, especially in terms of the Florian Wirtz example. I'm hoping to prove the media wrong! 😁

![Stop Florian Wirtz Abuse](images/florian.jpeg "florian.jpeg")
