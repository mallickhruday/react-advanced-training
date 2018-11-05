# Exercice 2 : Styled components

## Instructions

Nous souhaitons réaliser une application permettant de découvrir des films et de les mettre en favoris. Un peu comme Netflix sans la partie vidéo.

Nous allons commencer par créer les composants nécessaires à l'affichage d'une liste de films.

- Installer `styled-components @smooth-ui/core-sc`
- Créer un fichier `src/movies.json` avec la liste de films
- Créer un dossier `src/components`
- Créer un composant `MovieCard` qui affichera la carte d'un film
- Créer un composant `MovieList` qui affichera une liste de films
- Modifier le composant `App` pour afficher la liste de films

**Résultat attendu**

![Résultat](ex-2-result.png)

## Aide

```json
[
  {
    "vote_count": 6471,
    "id": 198663,
    "video": false,
    "vote_average": 7,
    "title": "The Maze Runner",
    "popularity": 464.010332,
    "poster_path": "/coss7RgL0NH6g4fC2s5atvf3dFO.jpg",
    "original_language": "en",
    "original_title": "The Maze Runner",
    "genre_ids": [28, 9648, 878, 53],
    "backdrop_path": "/lkOZcsXcOLZYeJ2YxJd3vSldvU4.jpg",
    "adult": false,
    "overview": "Set in a post-apocalyptic world, young Thomas is deposited in a community of boys after his memory is erased, soon learning they're all trapped in a maze that will require him to join forces with fellow “runners” for a shot at escape.",
    "release_date": "2014-09-10"
  },
  {
    "vote_count": 6124,
    "id": 346364,
    "video": false,
    "vote_average": 7.1,
    "title": "It",
    "popularity": 438.236716,
    "poster_path": "/9E2y5Q7WlCVNEhP5GiVTjhEhx1o.jpg",
    "original_language": "en",
    "original_title": "It",
    "genre_ids": [18, 27, 53],
    "backdrop_path": "/tcheoA2nPATCm2vvXw2hVQoaEFD.jpg",
    "adult": false,
    "overview": "In a small town in Maine, seven children known as The Losers Club come face to face with life problems, bullies and a monster that takes the shape of a clown called Pennywise.",
    "release_date": "2017-09-05"
  },
  {
    "vote_count": 1842,
    "id": 353486,
    "video": false,
    "vote_average": 6.4,
    "title": "Jumanji: Welcome to the Jungle",
    "popularity": 409.913886,
    "poster_path": "/bXrZ5iHBEjH7WMidbUDQ0U2xbmr.jpg",
    "original_language": "en",
    "original_title": "Jumanji: Welcome to the Jungle",
    "genre_ids": [28, 12, 35, 10751],
    "backdrop_path": "/cpz070zEKbPGXzCWuQsNt42PqXY.jpg",
    "adult": false,
    "overview": "The tables are turned as four teenagers are sucked into Jumanji's world - pitted against rhinos, black mambas and an endless variety of jungle traps and puzzles. To survive, they'll play as characters from the game.",
    "release_date": "2017-12-08"
  },
  {
    "vote_count": 6578,
    "id": 245891,
    "video": false,
    "vote_average": 7,
    "title": "John Wick",
    "popularity": 334.829619,
    "poster_path": "/5vHssUeVe25bMrof1HyaPyWgaP.jpg",
    "original_language": "en",
    "original_title": "John Wick",
    "genre_ids": [28, 53],
    "backdrop_path": "/umC04Cozevu8nn3JTDJ1pc7PVTn.jpg",
    "adult": false,
    "overview": "Ex-hitman John Wick comes out of retirement to track down the gangsters that took everything from him.",
    "release_date": "2014-10-22"
  }
]
```

```js
// App.js
import React, { Component } from 'react'
import styled, { createGlobalStyle } from 'styled-components'
import { globalStyle } from '@smooth-ui/core-sc'
import movies from './movies.json'
import MovieList from './components/MovieList'
import MovieCard from './components/MovieCard'

const GlobalStyle = createGlobalStyle`
  ${globalStyle()}

  body {
    background-color: #141414;
  }
`

const Header = styled.header`
  font-size: 40px;
  font-weight: 800;
  text-align: center;
  background-color: black;
  color: #d32f27;
  padding: 20px;
  text-transform: uppercase;
`

class App extends Component {
  render() {
    return (
      <div>
        <GlobalStyle />
        <Header>Smoothflix</Header>
        <MovieList>{/* TODO */}</MovieList>
      </div>
    )
  }
}

export default App
```

```js
// MovieCard.js
import React from 'react'
import styled from 'styled-components'

const Container = styled('div')`
  background-color: rgba(0, 0, 0, 0.2);
  background-image: url('${props => props.bgImg}');
  background-repeat: no-repeat;
  background-blend-mode: darken;
  background-position: center;
  background-size: 100%;
  height: 200px;
  color: white;
  position: relative;
  cursor: pointer;
  transition: background-size 300ms;

  &:hover {
    background-size: 140%;
  }
`

const InnerContainer = styled('div')`
  position: absolute;
  padding: 10px;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  opacity: 0;
  transition: opacity 500ms;

  &:hover {
    opacity: 1;
  }
`

const Title = styled('div')`
  font-size: 20px;
  font-weight: 300;
  margin-bottom: 8px;
`
const Vote = styled('div')`
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 8px;
`

const Overview = styled('div')`
  font-size: 14px;
`

const MovieCard = ({ movie }) => (
  <Container bgImg={`http://image.tmdb.org/t/p/w780/${movie.backdrop_path}`}>
    <InnerContainer>
      <Title>{movie.title}</Title>
      <Vote>{movie.vote_average} / 10</Vote>
      <Overview>{movie.overview}</Overview>
    </InnerContainer>
  </Container>
)

export default MovieCard
```

```js
// MovieList.js
import React from 'react'
import { Row, Col } from '@smooth-ui/core-sc'

const MovieList = ({ children }) => (
  <Row>
    {React.Children.map(children, (child, index) => (
      <Col md={4} key={index}>
        {child}
      </Col>
    ))}
  </Row>
)

export default MovieList
```