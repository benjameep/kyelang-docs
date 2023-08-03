---
title: "Dream Big - Data Package Management"
date: 2023-08-02T15:37:57-06:00
draft: true
---

Data Engineering is a lot of moving data around, making sure that data dependencies are met, and overall managing the flow of data. For example if you want to pull some data from a SaaS's api into your database so that you can do some reporting. It would be naive to think that a small little python script would suffice (especially from a maintainability perspective). You have to be able to answer questions such as:
- How are you authenticating with the api? Do you need a service account or permissions to create an api key?
- Are you incrementally loading the data or doing a full refresh everyday?
- How are you scheduling the job?
- How are you monitoring the job to make sure it ran successfully?
- How will you know if changes to the api are made?

But what if we could get rid of all that complexity and really make it so that it is as simple as writing a little python script? 

Hear me out, what if we thought of every data source & transformer as a "package", like in package managers for software engineering. The data source packages would specify how to configure their environment, authentication, data types, etc. The transformer packages would specify the data types they ingest, and their output data types.

These packages would be hosted in an environment for each company. If the environment could be trusted enough, it could even store the database credentials, api refresh tokens, etc. So that when you want to pull data, you log into the hosted environment, your access is checked, and then it can pull data from the data sources on your behalf without you having to track down credentials.

Or if it is too complicated to be able to run any source/transformer code on demand, then it could use your data warehouse as a sort of "cache". Where the results of your data source and transformers are saved in your data warehouse for any dependencies to pull.

Let's say the api you are pulling from is the [pokemon api](https://pokeapi.co/). Your data source script could look something like this:

    import requests
    from kye import Pokemon

    @kye.get
    def get_pokemon(id: Pokemon.id) -> Pokemon:
      return requests('https://pokeapi.co/api/v2/pokemon/' + id).json()
    
And the kye file would look like this:

    Pokemon(id: Number) {
      name: String
      weight: Number
      height: Number
      base_experience: Number
      types: PokemonType+
      abilities: PokemonAbility+
    }

