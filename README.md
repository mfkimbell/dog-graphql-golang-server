# dog-graphql-golang-server


Run the graphQL Server:

`go run server.go`

Run the graphQL Golang Integration:

`go get github.com/99designs/gqlgen@v0.17.49`

`go run github.com/99designs/gqlgen`


MySQL docker command:

`docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=dbpass -e MYSQL_DATABASE=hackernews -d mysql:latest`

https://www.howtographql.com/graphql-go/4-database/

Automatically "get" libraries: 

` go mod tidy `


Other facts:
* context, used to timeout actions like database connections so they don't run inifinitely, prevents resource leaks
* 

```golang
func (db *DB) Save(input *model.NewDog) *model.Dog {
	collection := db.client.Database("animals").Collection("dogs")
	ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
	defer cancel()
	res, err := collection.InsertOne(ctx, input)
	if err != nil {
		log.Fatal(err)
	}
	return &model.Dog{
		ID:        res.InsertedID.(primitive.ObjectID).Hex(),
		Name:      input.Name,
		IsGoodBoi: input.IsGoodBoi,
	}
}
```
* this (db *DB) is a method reciever, it calls this method on data of this type
* *DB is a pointer to the DB type
