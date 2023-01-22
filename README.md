# Functionality

## Movie List

I chose [json-server](https://www.npmjs.com/package/json-server) for simple REST API operations due to project scope and time constraint. It supports filter/pagination/sort which should be enough for storing movie info. The data from CSV file would be converted to JSON format, and when storing data some fields would be explicitly cast to number so they can be properly sorted. All movie items have ID auto-generated.

## Search

Users can type name for filtering movie list, and the search box had been handled by debounce so it would not fire too many API calls for every keystroke. json-server has a operator to match field by RegExp so it would try to return movies which have the search text in name. The movie list can be sorted in UI by user score, rating, and release year as a bonus.

## Details View

I chose to show movie details view by modal instead of page navigation, since there is not much to show for each movie, and it could improve UX when users would like to navigate among movies without having to load the main page every time, and kept the workflow simple. In the modal, users can view all fields of a movie and a comment section.

## Comment

All comment items in database have a movie ID field for which movie it is attached to. Then UI can load the comment list by filtering in API call based on the current movie ID in the modal. In UI, Angular's formGroup is applied here for user input to send a comment. We would have basic support like security (prevent XSS), validation from the framework.

## Nice to have

As mentioned earlier the application has movie list sorting to improve UX. Also there is a dark mode button on the top right as a bonus feature: ThemeService would check if preference is stored in local storage to apply theme, and toggle dark mode accordingly.

# Run in Docker

1. docker run -d -it -p 4200:80/tcp --name movie-app zoroaster00/movie-app:latest
2. docker run -d -it -p 3000:8080 --name movie-db zoroaster00/movie-db:latest
3. open [http://localhost:4200/](http://localhost:4200/)

# What can be improved

## i18n, l10n

- library and service for different language support
- currency localization (Worldwide Gross)

## Scale

- UI: if data is large, it should handle with pagination/infinite scrolling
- database: other database choices (mysql) based on use case and performance requirement
- API: in list page we do not need to display all the fields in movie, either change REST API to return name only or change backend to GraphQL

## UI

- RWD: the page should display well on all devices. The good news is Tailwind CSS is already used in the project so this should be easily handled.
- Item list: movies can be displayed in card view if there are images to display as well. Again, larger number of items need to be handled with pagination/infinite scrolling.
- Comment: it is common for comment feature to have "like", "reply" or other advanced actions. The database and model need to be re-designed though.

## Developer Experience

- Script to automatically fetch data from CSV and dump it into database
- CI/CD to run tests using docker

