<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>
  
<p align="center">A progressive <a href="http://nodejs.org" target="blank">Node.js</a> framework for building efficient and scalable server-side applications, heavily inspired by <a href="https://angular.io" target="blank">Angular</a>.</p>



# Architecture of NestJS

main.ts -> app.module.ts -> Controllers -> Services

## main.ts

It creates **AppModule**

## app.module.ts

AppModule is the class with Decorator(@). **Decorator** is a function on top of a class, and it dose something for a class. 
**controllers** call url and execute functions like routers in express.js.

```ts
@Module({
  imports: [],
  controllers: [MoviesController],
  providers: [MoviesService],
})
export class AppModule {}
```

## Controllers

```bash
# Generate a new controller
$ nest g co
# it will ask what name would be for the new controller
# created and imported everything automatically
```

Controllers get urls and return functions which are originally from Services. Get decorator (@Get()) is like routers (app.get('/url')) in express.js. @Post, @Delete, @Patch

```ts
@Controller()
export class MoviesController {
  constructor(private readonly moviesService: MoviesService) {}

  @Get()
  getAll(): Movie[] {
    return this.moviesService.getAll();
  }
  @Get('/:id')
  getOne(@Param('id') id: string): Movie {
    return this.moviesService.getOne(id);
  }
}
```

## Services

```bash
# Generate a new service
$ nest g s
# it will ask what name would be for the new service
# created and imported everything automatically
```

Services have a business logic and actual functions.

```ts
@Injectable()
export class MoviesService {
  private movies: Movie[] = [];

  getAll(): Movie[] {
    return this.movies;
  }
  getOne(id:string): Movie {
    const movie = this.movies.find(movie => movie.id === +id);
    if(!movie) {
      throw new NotFoundException(`Movie with ID ${id} not found.`);
    }
    return movie;
  }
}
```

# Insomnia
Used [insomnia core](https://insomnia.rest/) to test



---



## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

  Nest is [MIT licensed](LICENSE).
