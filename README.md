### Dataset 🧾
The Dataset that we used for this task is the [goodbooks-10k](https://github.com/zygmuntz/goodbooks-10k) dataset. It consists of 10k books with a total of 6 million ratings. That's huge right! 😮. There are some more huge datasets such as [Book-Crossings](http://www2.informatik.uni-freiburg.de/~cziegler/BX/) but they are kinda old 😬.

**Dataset Structure** 
```
GoodBooks10k 
    ├── books.csv         # Contains book info with book-id                         
    ├── ratings.csv       # Maps user-id to book-id and rating  
    ├── book_tags.csv     # Contains tag-id associated with book-ids
    ├── tags.csv          # Contains tag-name associated with tag-id
    ├── to_read.csv       # Contains book-ids marked as to-read by user  
```

### PreProcessing 🛠
Since this is a recommendation problem, we have to make sure that the `books.csv` is as clean as possible and only consider those ratings whose book-id is present, same goes for vice versa.

More Cleaning for `books.csv`
- Missing Book Image URLs
- Book & Rating Duplicates

### Model Exploration 🤯
For Recommendation Problems there are multiple approaches that are possible:
- Embedding Matrix
- Singular Matrix Decomposition
- Term Frequency

We experimented with several methods and chose Embedding Matrix & Term Frequency.

- **Embedding Matrix** - This method is often called [FunkSVD](https://www.coursera.org/lecture/matrix-factorization/deriving-funksvd-lyTpD) which won the Netflix Prize back in 2004. Since it is a gradient based function minimization approach we like to call it as Embedding Matrix. Calling it SVD [confuses](https://www.quora.com/What-is-the-difference-between-SVD-and-matrix-factorization-in-context-of-recommendation-engine/answer/Luis-Argerich) it with the one in Linear Algebra. This Embedding Matrix constructs a vector for each user and each book, such that when the product is applied with additional constraints it gives us the rating. For more elaborate info on FunkSVD refer [this](http://sifter.org/~simon/journal/20061211.html). 
We used the book embedding as a representation of the books to infer underlying patterns. This led to the embedding able to detect books from the same authors and also infer genres such as Fiction, Autobiography and more.

- **Term Frequency** - This method is like a helper function to above, it shines where embedding fails. Term Frequency takes into account the tokens in a book title be it the book title itself, the name of authors and also rating. Taking into consideration it finds books which match closely with the tokens in the rated book.

### Final Result
The [Image](https://coggle.it/diagram/X6TOUxlMvSl8FBM4/t/dataset/7083ac4f2de39517a4d97cd9d3d211c11af6e65f9a0034c46d613ff0f9cd5) says it All.

![coggle](https://user-images.githubusercontent.com/45713796/98331008-ae95e200-2021-11eb-915b-892854f88a6e.png)


### Project Structure
```
Kitabe
│   
├───BookRecSystem               # Main Project Directory
│       
├───mainapp                     # Project Main App Directory
│   │   
│   └───migrations              # Migrations
│           
├───static          
|   |                           # Static Directory
│   └───mainapp
│       ├───css                 # CSS Files  
|       |                         
│       ├───dataset             # Dataset Files
│       │       
│       ├───gif                 # GIF Media
│       │       
│       ├───model_files         # Model Files
|       |   |      
│       │   ├───surprise        # FunkSVD Files
│       │   │       
│       │   └───cv              # CV Files
│       │           
│       └───png                 # PNG Media FIles
|           
└───templates                   # Root Template DIrectory
    |
    ├───account                 # Account App Templates
    │       
    └───mainapp                 # Project Main App Templates
               
```   
