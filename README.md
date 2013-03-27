module Main where

import Control.Monad
import Data.List (isPrefixOf)  
import Data.Map
import System.Exit 
import System.IO
import System.IO.Error --Not used yet. Where do I want to go with handling, Ctrl-c (C-c) etc. ????


--ZXV by M. Zachary Kozatek aka ZachK 


myMap :: Map Integer String
myMap = fromList myMapList
  where
  myMapList :: [(Integer,String)]
  myMapList = []


main :: IO () 
main = loop 0 myMap 


seperator :: String
seperator = ": " 


newLine :: IO ()
newLine = putStrLn "" 


also :: IO a -> IO b -> IO ()
also a b =  a >> b >> return () 


goto :: (a -> b) -> a -> b 
goto a b = a b 


exitWithSuccess :: IO a 
exitWithSuccess = exitSuccess 


myExit :: IO Integer -> Map Integer String -> IO () 
myExit lineCount myMap = do --A bunch of stuff here, but for now we will just
  exitWithSuccess


loop lineCount myMap = do 
  --what is the current line count?
   line <- getLine 
   when ("exit" `isPrefixOf` line) `goto` (myExit lineCount myMap) 
   --append the current line count to the line
   --write it out
   let thing = show lineCount ++ seperator{-what is the seperator?-} ++ line
   putStrLn thing `also` print myMap `also` newLine 
   loop (lineCount + 1) (insert lineCount line myMap) 



