---
title: "Data Pipeline Frameworks"
date: 2023-08-02T15:37:57-06:00
---

Data Engineering is a lot of moving data around, making sure that data dependencies are met, and overall managing the flow of data. For example, let's say you want to pull data from a SaaS API into your database so that you can do some custom reporting. It would be naive to think that a simple python script making http requests would suffice (especially from a maintainability perspective). In order to have a data pipeline that is reliable and maintainable in the years to come, you need to be able to answer questions such as:
- How are you authenticating with the api? Do you need to create an api key or service account?
- Are you incrementally loading the data or doing a full refresh everyday?
- How are you scheduling the job?
- How are you monitoring the job to make sure it ran successfully?
- How will you know if changes to the api are made?

I believe there is the potential to simplify a lot of this complexity by creating a framework for data pipelines. Making it so that someone without much data engineering experience has a much better chance at succeeding.

## So what would this pipeline framework look like?

Here are the 6 steps that occur in a data pipeline (with examples):
1. **Authenticate** with the data provider
    - Check that your API key is still valid
    - Do OAuth handshake for access token
2. **Locate** the records you want to download
    - Specify the location of the database/schema/table
    - Filter for records you haven't extracted yet
3. **Pull** the records into memory
    - Parallelize requests for faster pulling
    - Bottleneck requests to not exceed a rate limit
4. **Validate** the contents contain what you expected
    - Check for any 404 (not found) or 500 (server errors)
    - Check that the data schema hasn't changed
5. **Transform** the data to fit in storage
    - Flatten json records for tabular storage
    - Parse timestamps
6. **Load** the records into your storage
    - Update existing records based on a primary key
    - Drop all existing data and load the new records (full refresh)

Sometimes you can skip a step, like authentication if your data source is public, or using an sdk library allows you to ignore how the data is being pulled. But there are usually decisions to be made along every step of the process.

The first four steps depend heavily on the type of data source you are pulling from. Which means that two different data pipelines built at different companies but pulling from the same type of data source will look very similar for those first 4 steps. Which means there is the opportunity to use someone else's code to accomplish those first 4 steps. And indeed we see companies like AirByte or Fivetran that will sell you a suite of prebuilt integrations.

The problem is that the way you transform your data depends heavily on your use case (which fields to keep, which fields to group by etc.) So these prebuilt integrations make a minimal amount of assumptions and shove the raw data into your data warehouse (known as ELT). This can have benefits in the short term, getting you up to speed faster, but resembles a "hoarding" behavior. Where if you aren't careful, your house will fill up with random junk you don't need.

This is where Kye comes in. It aims to be a framework for validating and transforming raw data into a more useful form. Where you can have peace of mind knowing that the raw data isn't going to break your transformations, and you'll have a standard method of loading data into your storage and keeping it up to date.