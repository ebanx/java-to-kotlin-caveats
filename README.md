# Java to Kotlin - Caveats
This is a document to register problems found while changing a production software from Java to Kotlin. Fell free to add your contribution. 

## Tests
#### Mockito
You can't use Mockito to mock your POJOS by mocking your getters using Kotlin. You need to create your mocks of POJOs by hand. It happens because data classes are final in Kotlin, you can't use the Open modifier in then. 

Also, you need to rely in the dependency inversion principle in order to be able to test your code, because all classes and methods in Kotlin are final by default. This is actually a really great thing, but be aware about this, you won't be able mock concrete classes, rely on abstractions!

#### Bugs in tests
Using the Android Studio 2.3.2 you can't run a single test... You need to run all the tests in the package at one. 


## Databinding
You need to annotate your methods in the adapters with @JvmStatic. Ex:

    @JvmStatic
    @BindingAdapter("setText")
    fun setText(button: Button, state: Enum) {
          //your logic here!
    }

If you don't do so, this can lead to really hard tracking bugs. 

## Dagger 2
Don't use implicit type in your DaggerModules. Like this:

    @Provides
    @Singleton
    internal fun provideSomeClass() = SomeClass()

You need to set the type explicitly. 

## Good practices 
#### Databinding
When using Databinding, use ObservableField in Kotlin is a good pratice because you don't have to deal with getters and setters in Kotlin. 

#### Robot Pattern
The Robot Pattern looks a lot better in Kotlin! If you don't this pattern, you can check it out here: https://news.realm.io/news/kau-jake-wharton-testing-robots/. 

#### Test Coverage
Substitute your POJOs in Java for data classes in Kotlin will allow your coverage tool to focus in code that contains important logic, instead of POJOs. This allows the dev team to have a clearer idea about how well the code really is

> Written with [StackEdit](https://stackedit.io/).
