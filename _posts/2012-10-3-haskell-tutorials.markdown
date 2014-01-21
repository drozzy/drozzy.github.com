---
layout: post
title: Tutorial on How to write a Haskell Tutorial
tags: [programming]
---

Over the course of reading many tutorials and examples for Haskell and it's libraries,
I can say that there are some things that are an absolute requirement for
making it easier for readers to understand your code. Here are the things
I think should be in every tutorial or teaching example of Haskell code.

Explicit Imports
================
This is so important that it has to be #1. To be able to figure out where a given type or function
comes from, always full qualify what you are importing from where.

For example, in the code below, where do the functions ask and put and the types Query and Update come from?

    module Test where 

    import Data.Acid
    import Control.Monad.State
    import Control.Monad.Reader

    data MyState = MyState String deriving (Show)

    writeState :: String -> Update MyState ()
    writeState val = put (MyState val)

    queryState :: Query MyState (Maybe String)
    queryState = do MyState str <- ask
		    return $ Just str


Now if we write it like this, things become much clearer:

    module Test where 

    import Data.Acid (Update, Query)
    import Control.Monad.State (put)
    import Control.Monad.Reader (ask)

    data MyState = MyState String deriving (Show)

    writeState :: String -> Update MyState ()
    writeState val = put (MyState val)

    queryState :: Query MyState (Maybe String)
    queryState = do MyState str <- ask
		    return $ Just str



which brings me to the next point.

Explicit Imports of Prelude types
==================================
You may know that Maybe monad is imported by the Prelude, but most of the new users will often
get confused. So, yes, import the Prelude types and functions explicitly.

    import Data.Maybe (Maybe)
    import Data.Acid (Update, Query)
    import Control.Monad.State (put)
    import Control.Monad.Reader (ask)

    data MyState = MyState String deriving (Show)

    writeState :: String -> Update MyState ()
    writeState val = put (MyState val)

    queryState :: Query MyState String
    queryState = do MyState str <- ask
		    return str


Put Source in Single File
==========================
When a new user is getting acquainted with the new library or framework, the last thing he needs 
to worry about is file or module structure. The user needs to see how components interact with each
other. Keeping all the source code in one file (even if long) allows the user to quickly to a text
search for a relevant piece of code.

Later tutorials or examples may show the best way to structure the application. In fact, this is what
most frameworks provide in a form of starter app or a project template.

Err on the side of More Comments
================================
Even if you are writing a tutorial, and showing snippets of code, it does
not hurt to put comments in that code as well. For example:

    -- We'll need this for return types
    import Data.Maybe (Maybe)
    -- Basic return types for our pure query functions
    import Data.Acid (Update, Query)
    -- These will allow use to manipulate state
    import Control.Monad.State (put)
    import Control.Monad.Reader (ask)

    -- What we will persist
    data MyState = MyState String deriving (Show)

    -- Store a string in a state
    writeState :: String -> Update MyState ()
    writeState val = put (MyState val)

    -- Retrieve a maybe value from the state.
    queryState :: Query MyState String
    queryState = do MyState str <- ask
		    return str

while this code may be a nightmare to read or maintain in a real application or for a professional
Haskell developer -- to a newbie every line is like a piece of gold, clarifying some concepts
he or she didn't completely grasp or understand.

Provide Library Versions
==========================

For every library that you import or reference, provide an exact version that the code you wrote 
will run with. Haskell is a fast developing ecosystem, and things get broken all the time. For a newbie
it is not important that they work with the latest libraries when learning. All they needs is to grasp
the concepts and ideas. After which they will be able to go out on their own and infer how these things
should work in future versions.

The easiest way to satisfy this requirement would be to include .cabal file with
your tutorial or example, which has the Build-depends directive. You can easily and interactively create a
.cabal file for you code with the following command, which you should run inside your source code directory:
 
    cabal init

Explain Difficult Type Signatures
=================================

One of the most difficult things for a newbie to figure out is all the types everywhere.
So when you have a complicated looking type, take your type to explain what is going. 

For example, Acid State tutorial does a great job with this when they explain this type
signature:

     update' :: (UpdateEvent IncCountBy, MonadIO m) =>
                 AcidState (EventState IncCountBy)
                 -> IncCountBy
                 -> m (EventResult IncCountBy)

and here is the explanation:

> EventState is a type function. EventState IncCountBy results in the type CounterState. So that reduces to AcidState CounterState. So, we see that we can not accidently call the IncCountBy event against an acid state handle of the wrong type.

