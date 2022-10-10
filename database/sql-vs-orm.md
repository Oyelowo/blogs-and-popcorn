# Is it easier to write and maintain pure SQL over an ORM?

ORMs and Query Builders IMO are symptoms of inadequate toolings which modern engineering has inadequately addressed.

Most Engineers would admit that pure SQL is far easier to grok, in addition to being transferable.

Typically, I see this done every time:

1. Engineer writes a complex pure SQL ->
2. translates that to ORM/Query builder’s DSL ->
3. Tests that the query builder properly generates what had already initially been written.

As you can see, this adds an unnecessary layer of indirection and cognitive overhead, and many query builders don’t even properly generate the right SQL when dealing with complex queries. So, engineers are left to write unchecked queries.

But what if we can eliminate the latter while retaining the simplicity of SQL and the flexibility and type-checking that ORMs and query builders provide?

SQLx in Rust got many things right but it still has the trade-off of requiring a life database connection or upfront query compilation/caching from the database. In addition, it only works for a few RDBMS.

But what if we can retain SQL’s beauty without the overhead of translation or requiring a database connection? I did a proof-of-concept over a weekend in #june specifically for #mongodb but turns out I could use the same implementation for other databases.

Since then, I’ve been using it for #postgresql and now #surrealdb. It does the type-checking of the SQL queries and validation of referenced fields. The solution requires a combination of procedural and declarative #macros in #Rust.

So, now I get to write pure SQL everywhere without sinking time into learning new DSLs for every ORM I would otherwise have used.

I intend to open-source this before the year runs out. And will Livestream the implementation.