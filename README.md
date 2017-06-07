#Java to Kotlin - Caveats
This is a document to register to problem found while changing a production software from Java to Kotlin. Fell free to add your contribution. 

## Tests
#### Mockito
You can't use Mockito the mock your POJOS mocking the getters of the class using Kotlin. You need to create your mocks of POJOs by hand. It happens because data classes are final in Kotlin, you can't use the Open modifier in then. 

Also, you need to really hardly in the dependency inversion principle in order to be able to test your code, because all classes and methods in Kotlin are final by default. This is actually a really great thing, but be aware about this. 

#### Bugs in tests
Using the Android Studio 2.3.2 you can't run a single test... You need to run all the tests in the package at one. 


## Databinding
You need to annotate your methods in the adapters with @JvmStatic. Ex:

    @JvmStatic
    @BindingAdapter("setText")
    fun setText(button: Button, state: Enum) {
          //your logic here!
    }

If you don't do so, this can lead to really hard tacking bugs. 

## Dagger 2
Don't use implicit type in your DaggerModules. Like this:

    @Provides
    @Singleton
    internal fun provideSomeClass() = SomeClass()

You need to set the type explicitly. 

## Good practices 
When using Databinding, use ObservableField in Kotlin is a good pratice because you don't have to deal with getters and setters in Kotlin. 

The Robot Pattern looks a lot better in Kotlin! If you don't this pattern, you can check it out here: https://news.realm.io/news/kau-jake-wharton-testing-robots/. 

> Written with [StackEdit](https://stackedit.io/).