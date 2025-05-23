---
title: Weather Cards
date: 2025-04-04 12:00:00 +0700
description: A minimal weather web app built with raw HTML/CSS/JavaScript.
categories: [Software, Web Development]
tags: [html, css, javascript, api, serverless-function]
pin: true
---

## Live Demo

[Click here to try the weather app.](https://puth2314.github.io/weather-cards/)

## Design Choices

1. Should a there a title/heading in the website?
   - I chose no, because the website is relatively simple and a title/heading would take up quite a bit of space making the overall website feel unbalanced. In addition, I hope the feel and functionaility of the website explain itself well.
2. How to handle not revealing the API-key to public?
3. Why is `form` chosen over another `div`?
   - It works when also pressing the `Enter` key, instead of solely just working when clicking a button.
4. How to choose the order of temperature, weather icon, and weather description to be shown?
5. Why specifically choose to display cloud percentage and wind speed, but not say himidity.
6. How should we choose the colors for the weather details (cloud percanta, wind speed, etc.)?
7. How many forecasts should be shown?

## To-Do

- [ ] Make the foreground (`main`) expand first, then show the content (`results-container`).
- [ ] Dark mode.
- [ ] Mobile view.
- [ ] Autocomplete/suggestions of bad city names.
- [ ] Phrases for locations in placeholder.
- [ ] Figure out how to handle typing during transition/animation.
- [ ] Figure out how to handle inputs during transition/animation.
- [ ] Make it embeddable.
- [ ] Be able to read user location.
- [ ] Make the transitions/animations cleaner, some elements are changing during animation.
- [x] Fix overlapping animations.
- [x] ~~Bootstrap or another UI framework.~~ (Not needed for this scale)
- [x] Add weather forecasts.
- [x] Icons for weather.
- [x] Better error for wrong city names.
