**API Driven Design** by [Eric Stern](https://twitter.com/Firehed)

MVC frameworks gives you fast prototyping and reasonably sane architecture.  But the structure is inflexible, things are tightly coupled, and it's unsuitable for non-web tasks.  Alot of routing systems are designed are semantics for HTTP.  And they are mostly are bundled with the active record pattern for models.

What does every API need?

* Authentication
* Request and response formats
* Documentation

* SDK
* Sandbox
* Versioning
* Simulator Tools
* Testing
* Logging

**Think in Libraries**

* Put SDKs and interfaces in their own repositories
* Import as needed - avoid huge frameworks
* Develop independently

**Writing Tests**

Writing tests for everything is hard...because writing testable code is hard.  When code is not testable you don't test it.

Think about what you want to get out of your code when you make it testable.

Just because a class implements an interface it doesn't mean that's all it exposes.

By focusing on interfaces during design phase you can make sure they make sense for what you're doing.

Use the testing process as a way to make sure you're library is good.

"A singleton is basically just a wrapper for global state."

Focus on making small classes with more methods that do less things each.

**Deployment**

1. Install Dependencies
2. Compile & compress
3. Run tests
4. Push the build
5. Flip it live

"The more often you deploy, the easier deployments become."