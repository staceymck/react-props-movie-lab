# React Simple Props Movie Lab

## Objectives

- Practice passing props from parent components to children

## Introduction

This is a bare-bones React application used to showcase the nine greatest movies
of all time. Our job is to update it so that it passes props from the parent to
children components correctly. In addition, we will implement default props so
that 'bad/missing data' is properly handled - preventing our user interface from
blowing up our visitors' computers

Following is the component tree. When fully rendered, there are **9**
`MovieCards` rendered by `MovieShowcase`:

```text
└── MovieShowcase
    └─ MovieCard
       └─ CardFront
```

`MovieShowcase` is the component that will house all of the 'raw' data
associated with the movies we want to display. This data is located in
`src/data.js` and is already being imported.

`MovieCard` components (which showcase a single movie) receive their individual
movie information from `MovieShowcase` as two props: `title` and `genres`.
Following that, the props are passed again to `CardFront`.

In our movie data set, we occasionally have missing data. This is where
`defaultProps` come in and really pull our buns out of the fire. We will be
handling all of our `defaultProp`'ing in `MovieCard` before they are passed down
the chain to the front component.

## Deliverables

###### `MovieShowcase`

To get started, take a look at `src/data.js` to get a sense of the data you'll
be working with. We can see that the data is stored in an array of objects. At
the end of this file, the data is set up to be exported and in
`src/MovieShowcase.js`, we can see that this data gets imported in at the top:

```js
import movieData from './data.js'
```

The `MovieShowcase` component, then, has access to `movieData`. We want to take this
data and, for every object inside, render a `MovieCard` component, passing the object
data in as props like so:

```js
generateMovieCards = () => {
  return movieData.map((movie, index) =>
    <MovieCard
      key={index}
      title={movie.title}
      genres={movie.genres}
    />
  )
};
```

In JSX, it is possible to include JavaScript code and calls to functions. A function
called in JSX must be wrapped in curly braces and must return either a single JSX element,
or an array that contains multiple JSX elements. A single JSX element, however, can contain
other elements.

This is what we are doing with `movieData`: mapping over the data and passing in values from
each object as props. See the [documentation here][lists-and-keys] for additional information.

Once we have our function that generates an array of MovieCard components we need to
invoke that function in our render function as mentioned above:

```js
render() {
  return <div id="movie-showcase">{this.generateMovieCards()}</div>;
}
```

###### `MovieCard`

If everything is set up properly in `MovieShowcase`, running the application
will produce a page with 9 empty squares on the page. These are the nine
`MovieCard` components being rendered in `MovieShowcase`.

If we were to place `console.log(this.props)` in the `MovieCard` component at
the beginning of `render()`, we'd see that each `MovieCard` contains different
props. Our next task here is to pass props to the child component of `MovieCard`,
`CardFront`.

`CardFront` will display the title and genres and therefore it should receive the
`title` and `genre` props. Lets take a look at how this works in action:

```js
render() {
  return (
    <div className="movie-card">
      <CardFront
        title={this.props.title}
        genres={this.props.genres}
      />
    </div>
  );
}
```

Thinking about the structure of this application, `CardFront` has a specific
task - to display the data it receives as props. `MovieShowcase` is where
this data is imported in. What is the purpose of `MovieCard` then?

In this case, `MovieCard` acts as a sort of container. It does render a `div`
element with a CSS class, but besides that, its primary purpose is to house
the `CardFront` component.

Besides containing `CardFront`, the `MovieCard` component can also be used to
make sure that the data being passed down to `CardFront` is complete. For this,
we can use default props. Default props allow us to set a default value in the
event that a prop is not provided. By doing this in `MovieCard`, we can ensure
that the props passed down to `CardFront` are consistent.

Lets write `defaultProps` like this:

```js
MovieCard.defaultProps = {
  title: 'Unknown',
  genres: ['No Genre(s) Found'],
};
```

Review the previous Props readme for an example on default props, and/or take a
look at the [documentation][default props] for additional guidance.

###### `CardFront`

In this component, we need to render the `title`, `genres`. Remember that `genres`
is an array of multiple genres so we will have to join them into a single string
separated by commas. Lets take a look at how to do that:

```js
render() {
  return (
    <div className="card">
      <h3 className="title">Title: {this.props.title}</h3>
      <h5 className="genres">Genre(s): {this.props.genres.join(', ')}</h5>
    </div>
  );
}
```

#### Once Finished

Check out the application and make sure everything is functioning how you would like!

## Resources

- [React Default Prop Values][default props]

[default props]: https://reactjs.org/docs/react-component.html#defaultprops
[lists-and-keys]: https://reactjs.org/docs/lists-and-keys.html

<p class='util--hide'>View <a href='https://learn.co/lessons/react-props-movie-lab'>Props Lab</a> on Learn.co and start learning to code for free.</p>
