# Lazy Initialization Approach: 

        Do follow the following steps.
        Create a class with Private constructor --- this allows the applications not to create its instance.
        add a private static variable of the class. --- static because the element gets created at class level rather than object level.
        Now add public method with singleton class return type. 
        
        class Singleton{
        
            private static Singleton instance;
            private Singleton(){}
            
            public static getInstance(){
                   if(Singleton.instance == null)
                     return instance = new Singleton();
                   else
                     return instance;
           }
        
        }
        
        Problems with above approach:   its not threadsafe -- in case of single threaded environment this is the better approach.



# Eager Initialization:

class Singleton{
        
            private static Singleton instance = new Singleton();
            private Singleton(){}
            
            public static getInstance(){
                   if(Singleton.instance == null)
                     return instance = new Singleton();
                   else
                     return instance;
           }
        
        }


# Thread safe (Inefficeient way):

      -- To make the class threadsafe, add synchronized to method getInstance().
   

        class Singleton{
        
            private static Singleton instance;
            private Singleton(){}
            
            public static synchronized getInstance(){
                   if(Singleton.instance == null)
                     return instance = new Singleton();
                   else
                     return instance;
           }
        
        }
  
          Problem with this approach is that it will hinder the performance of the class.  
          Adding synchronized to static method will make threads to aquire lock on class level and there can be only one lock per class instance. Lock will be acquired as soon as we enter the method and will be released after method end.
          
          But here we need only lock during null check.
          
          
          so add synchronization at block level will be a best approach.
  


# Thread safe (Efficient):

class Singleton{
        
            private static volatile Singleton instance;
            private Singleton(){}
            
            public static  getInstance(){
                 synchronized(Singleton.class){
                   if(Singleton.instance == null)
                     return instance = new Singleton();
                   }
                   else
                     return instance;
           }
        
        }



# Approach which prevents Singleton form Reflextion/Serialization/Cloning



