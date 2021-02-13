# Data Processing for NN Models 


### Encountering data 
  #### null data (missing values) 
      check to see if null values in dataset exist 
   #python : 
      df.isnull(). # --> returns boolean matrix, if value is NaN then True otherwise false
      df.isnull().sum() # --> returns column names with no. of NaN values in that column 
      
          ^^^ drop rows/columns that contain null values 
              df.dropna() 
                ** Note: this may lead to potential loss of valuable data. (higher amnt of data not as problematic)
#### Use Imputation to handle Null Data
  ### substituting missing values 
          custom function or **SimpleImputer*
          
          from sklearn.impute import SimpleImputer 
          imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
          imputer = imputer.fit(df[['Weight']])
          df['Weight'] = imputer.transform(df[['Weight']])
          

### Standardization 
  #### data is transformed : mean of values is 0 & standard deviation is 1 
        Calculate the mean and standard deviation of values   
            for each data point, subtract mean and divide by standard deviation 
            
         from sklearn.preprocessing import StandardScaler 
         std = StandardScaler()
         X = stf.fit_transform(df[['Age', 'Weight'']])
         
       **Note: standardize training AND testing data** 

### Categorical Variables 
  #### discrete not continuous 
        2 subtypes: 
                - Ordinal : can be Ordered
                 - Nominal : can't be Ordered 
                 
 ##### Ordinal and Nominal Categorical Variables need to be preprocessed differently 
 
 
#### Ordinal Categorical Variables 
  ### create dataframe 
  
 df_cat = pd.DataFrame(data = 
                     [['green','M',10.1,'class1'],
                      ['blue','L',20.1,'class2'],
                      ['white','M',30.1,'class1']])
df_cat.columns = ['color','size','price','classlabel']
                          
## Transform Ordinal CVS : 
  1. map() function 
      size_mapping = {'M':1, 'L':2}
       df_cat['size'] = df_cat['size'].map(size_mapping)
          
          *** M will be replaced with 1 and L with 2
           
  2. Using Label Encoder
    
      from sklearn.preprocessing import LabelEncoder
      class_le = LabelEncoder()
      df_cat['classlabel'] = 
      class_le.fit_transform(df_cat['classlabel'].values) 
      
           *** class1 presented with 0 and class2 with 1 
           
 ## Nominal Categorical Variables 
  ### One-Hot Encoding 
   ##### create 'n' columns. n --> number of unique values nominal variable can take.
  df_cat = pd.get_dummies(df_cat[['color', 'size', 'price']])
  
        ***get_dummies function will only consider string variables 
        
        
        
        
  #### Problems that can occur with One-Hot --> Multicollinearity 
   ###### Where features exist that are strongly dependent on each other 
            - won't be able to use weight vector to calculate feature importance 
             - impacts interpretability 
             
             df_cat = pd.get_dummies(df_cat[['color', 'size', 'price']], drop_first=True) 
