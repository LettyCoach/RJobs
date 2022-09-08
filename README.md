<h1 align="center">{Remotive Jobs}</h1>

<div align="center">
   Solution for a challenge from  <a href="http://devchallenges.io" target="_blank">Devchallenges.io</a>.
</div>

<div align="center">
  <h3>
    <a href="https://https://remotive-jobs.vercel.app/">
      Demo
    </a>
    <span> | </span>
    <a href="https://devchallenges.io/solutions/kc9bP1wkX1yLpb6Xjm1m">
      Solution
    </a>
    <span> | </span>
    <a href="https://devchallenges.io/challenges/TtUjDt19eIHxNQ4n5jps">
      Challenge
    </a>
  </h3>
</div>

<!-- TABLE OF CONTENTS -->

## Table of Contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Features](#features)
  - [How to use](#how-to-use)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## Overview

![screenshot](https://user-images.githubusercontent.com/68834718/189035104-aa71647e-33e4-442a-a2f9-c0d50bba2db1.png)

### The challenge

Users should be able to:

- User can see a list of jobs in a city by default
- User can search for jobs with a given keyword
- User can search for a full-time job only
- User can see a list of jobs with their logo, company name, location, and posted time.
- When user select a job, user can see job descriptions and how to apply like the given design.
- When user is on the job details page, user can go back to the search page
- User can see jobs on different pages, 5 items on each page

### Features

- App displays list of jobs
- App displays list of jobs according to the category specified
- App displays list of jobs according to the location specified
- App shows the jobs searched by the user

This application/site was created as a submission to a [DevChallenges](https://devchallenges.io/challenges) challenge. The [challenge](https://devchallenges.io/challenges/TtUjDt19eIHxNQ4n5jps) was to build an application to complete the given user stories.

### How To Use

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [yarn](https://yarnpkg.com) installed on your computer. From your command line:

```bash
# Clone this repository
$ git clone https://github.com/vatsalsinghkv/remotive-jobs

# Install dependencies
$ yarn

# Run the app
$ yarn dev
```

## My process

### Built With

- [Next.js](https://nextjs.org/) - Fullstack Framework
- [Sass](https://sass-lang.com/) - CSS pre-processor
- [Redux Toolkit](https://redux-toolkit.js.org/) - State Manager
- [Axios](https://axios-http.com/) - For HTTP requests
- [next-redux-wrapper](https://github.com/kirill-konshin/next-redux-wrapper) - A HOC that brings Next.js and Redux together
- [react-html-parser](https://www.npmjs.com/package/react-html-parser) - A utility for converting HTML strings into React components

### What I learned

I've learned lot of things in this challenge:

- How to use Redux toolkit for state management in nextjs

```js
// store/index.js
import { combineReducers, configureStore } from '@reduxjs/toolkit';
import { createWrapper, HYDRATE } from 'next-redux-wrapper';
import pagination from './pagination';
import jobs from './jobs';

const combinedReducer = combineReducers({
  pagination,
  jobs,
});

const masterReducer = (state, action) => {
  if (action.type === HYDRATE) {
    return {
      ...state,
      ...action.payload,
    };
  } else {
    return combinedReducer(state, action);
  }
};

const makeStore = () => {
  return configureStore({
    reducer: masterReducer,
  });
};

const wrapper = createWrapper(makeStore);
export { makeStore, wrapper };
```

```js
// pages/index.js
import { wrapper } from '../store';

export const getStaticProps = wrapper.getStaticProps((store) => async () => {
  const jobs = await getAllJobs();
  store.dispatch(setJobs(jobs));

  const categories = await getJobsCategories();
  store.dispatch(setCategories(categories));

  const locations = await getLocations();
  store.dispatch(setLocations(locations));

  store.dispatch(setSelectedCategory('all'));

  return {
    props: { jobs },
  };
});
```

- How to use getStaticPaths

```js
// pages/category/[category].js
export const getStaticPaths = async () => {
  const categories = await getJobsCategories();
  return {
    paths: categories.map((category) => ({ params: { category } })),
    fallback: false,
  };
};
```

### Continued development

Technologies I'd be learning soon:

- Typescript
- Data Structures and Algorithms
- Material UI
- Backend Development
- Blockchain Development
- Testing (JS)
- Flutter & Dart
- Cyber Security

### Useful resources

- [MDN Docs](https://developer.mozilla.org/en-US/) - This is an amazing reference which helped me finally understand detailed concepts like data- attr, aria attr, input range etc.
- [Nextjs Docs](https://nextjs.org/docs/getting-started) - Best reference to get start with Nextjs
- [Illustrations](https://storyset.com/) - Best illustrations for errors and warnings etc.
- [Logo/Icons](https://www.flaticon.com) - Flat Icons best place for free icons

## Contact

- Github - [@vatsalsinghkv](https://github.com/vatsalsinghkv)
- Twitter - [@vatsalsinghkv](https://www.twitter.com/vatsalsinghkv)
- Instagram - [@vatsal.sing.hkv](https://www.instagram.com/vatsal.singh.kv)
- Facebook - [@vatsalsinghkv](https://www.facebook.com/vatsal.singh.kv)
- devChallenges - [@vatsalsinghkv](https://devchallenges.io/portfolio/vatsalsinghkv)
- Frontend Mentor - [@vatsalsinghkv](https://www.frontendmentor.io/profile/vatsalsinghkv)

## Acknowledgements

- [Illustrations by Storyset](https://storyset.com/)
- [Favicon](https://www.flaticon.com/free-icon/search_4234031?related_id=4234031&origin=search)
