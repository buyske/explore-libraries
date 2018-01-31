

```r
## First attempt: Just get it to work ----

list.files("~/Desktop/day1_s1_explore-libraries")
```

```
## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
## [3] "01_explore-libraries_spartan.R"
```

```r
list.files("~/Desktop/day1_s1_explore-libraries", pattern = "\\.R$")
```

```
## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
## [3] "01_explore-libraries_spartan.R"
```

```r
list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)
```

```
## [1] "/Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R"  
## [2] "/Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R"  
## [3] "/Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R"
```

```r
from_files <- list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)

(to_files <- basename(from_files))
```

```
## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
## [3] "01_explore-libraries_spartan.R"
```

```r
file.copy(from_files, to_files)
```

```
## [1] FALSE FALSE FALSE
```

```r
list.files()
```

```
##  [1] "00_filesystem-practice_comfy.html"
##  [2] "00_filesystem-practice_comfy.md"  
##  [3] "00_filesystem-practice_comfy.R"   
##  [4] "00_filesystem-practice_jenny.R"   
##  [5] "00_filesystem-practice_jenny.Rmd" 
##  [6] "01_explore-libraries_comfy.R"     
##  [7] "01_explore-libraries_jenny.R"     
##  [8] "01_explore-libraries_spartan.R"   
##  [9] "explore-libraries.Rproj"          
## [10] "README.md"                        
## [11] "scratch.html"                     
## [12] "scratch.Rmd"
```

```r
## Clean it out, so we can refine ----
file.remove(to_files)
```

```
## [1] TRUE TRUE TRUE
```

```r
list.files()
```

```
## [1] "00_filesystem-practice_comfy.html" "00_filesystem-practice_comfy.md"  
## [3] "00_filesystem-practice_comfy.R"    "00_filesystem-practice_jenny.R"   
## [5] "00_filesystem-practice_jenny.Rmd"  "explore-libraries.Rproj"          
## [7] "README.md"                         "scratch.html"                     
## [9] "scratch.Rmd"
```

```r
## Copy again, tighter code ----
from_dir <- file.path("~", "Desktop", "day1_s1_explore-libraries")
from_files <- list.files(from_dir, pattern = "\\.R$", full.names = TRUE)
to_files <- basename(from_files)
file.copy(from_files, to_files)
```

```
## [1] TRUE TRUE TRUE
```

```r
list.files()
```

```
##  [1] "00_filesystem-practice_comfy.html"
##  [2] "00_filesystem-practice_comfy.md"  
##  [3] "00_filesystem-practice_comfy.R"   
##  [4] "00_filesystem-practice_jenny.R"   
##  [5] "00_filesystem-practice_jenny.Rmd" 
##  [6] "01_explore-libraries_comfy.R"     
##  [7] "01_explore-libraries_jenny.R"     
##  [8] "01_explore-libraries_spartan.R"   
##  [9] "explore-libraries.Rproj"          
## [10] "README.md"                        
## [11] "scratch.html"                     
## [12] "scratch.Rmd"
```

```r
## Clean it out, so we can use fs ----
file.remove(to_files)
```

```
## [1] TRUE TRUE TRUE
```

```r
list.files()
```

```
## [1] "00_filesystem-practice_comfy.html" "00_filesystem-practice_comfy.md"  
## [3] "00_filesystem-practice_comfy.R"    "00_filesystem-practice_jenny.R"   
## [5] "00_filesystem-practice_jenny.Rmd"  "explore-libraries.Rproj"          
## [7] "README.md"                         "scratch.html"                     
## [9] "scratch.Rmd"
```

```r
## Copy again, using fs ----
library(fs)
(from_dir <- path_home("Desktop", "day1_s1_explore-libraries"))
```

```
## /Users/peterhiggins/Desktop/day1_s1_explore-libraries
```

```r
(from_files <- dir_ls(from_dir, glob = "*.R"))
```

```
## /Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R
## /Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R
## /Users/peterhiggins/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R
```

```r
(to_files <- path_file(from_files))
```

```
## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
## 01_explore-libraries_spartan.R
```

```r
(out <- file_copy(from_files, to_files))
```

```
## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
## 01_explore-libraries_spartan.R
```

```r
dir_ls()
```

```
## 00_filesystem-practice_comfy.R    00_filesystem-practice_comfy.html 
## 00_filesystem-practice_comfy.md   00_filesystem-practice_jenny.R    
## 00_filesystem-practice_jenny.Rmd  01_explore-libraries_comfy.R      
## 01_explore-libraries_jenny.R      01_explore-libraries_spartan.R    
## README.md                         explore-libraries.Rproj           
## scratch.Rmd                       scratch.html
```

```r
dir_info()
```

```
##                                 path type    size permissions
## 1     00_filesystem-practice_comfy.R file   2.42K   rw-r--r--
## 2  00_filesystem-practice_comfy.html file     16K   rw-r--r--
## 3    00_filesystem-practice_comfy.md file    2.8K   rw-r--r--
## 4     00_filesystem-practice_jenny.R file   1.67K   rw-r--r--
## 5   00_filesystem-practice_jenny.Rmd file   1.69K   rw-r--r--
## 6       01_explore-libraries_comfy.R file   1.12K   rw-r--r--
## 7       01_explore-libraries_jenny.R file   1.54K   rw-r--r--
## 8     01_explore-libraries_spartan.R file   1.86K   rw-r--r--
## 9                          README.md file     136   rw-r--r--
## 10           explore-libraries.Rproj file     205   rw-r--r--
## 11                       scratch.Rmd file     838   rw-r--r--
## 12                      scratch.html file 695.33K   rw-r--r--
##      modification_time         user group device_id hard_links
## 1  2018-01-31 14:07:32 peterhiggins staff  16777220          1
## 2  2018-01-31 14:16:33 peterhiggins staff  16777220          1
## 3  2018-01-31 14:16:33 peterhiggins staff  16777220          1
## 4  2018-01-31 13:56:49 peterhiggins staff  16777220          1
## 5  2018-01-31 14:27:33 peterhiggins staff  16777220          1
## 6  2018-01-31 09:54:51 peterhiggins staff  16777220          1
## 7  2018-01-31 09:54:51 peterhiggins staff  16777220          1
## 8  2018-01-31 11:03:07 peterhiggins staff  16777220          1
## 9  2018-01-31 13:46:07 peterhiggins staff  16777220          1
## 10 2018-01-31 14:24:24 peterhiggins staff  16777220          1
## 11 2018-01-31 14:15:39 peterhiggins staff  16777220          1
## 12 2018-01-31 14:22:58 peterhiggins staff  16777220          1
##    special_device_id      inode block_size blocks flags generation
## 1                  0 8593524593    4194304      8     0          0
## 2                  0 8593525390    4194304     32     0          0
## 3                  0 8593525389    4194304      8     0          0
## 4                  0 8593524666    4194304      8     0          0
## 5                  0 8593532843    4194304      8     0          0
## 6                  0 8593532847    4194304      8     0          0
## 7                  0 8593532848    4194304      8     0          0
## 8                  0 8593532849    4194304      8     0          0
## 9                  0 8593524466    4194304      8     0          0
## 10                 0 8593524027    4194304      8     0          0
## 11                 0 8593525674    4194304      8     0          0
## 12                 0 8593526055    4194304   1408     0          0
##            access_time         change_time          birth_time
## 1  2018-01-31 14:24:25 2018-01-31 14:07:32 2018-01-31 11:22:12
## 2  2018-01-31 14:14:13 2018-01-31 14:16:33 2018-01-31 14:14:13
## 3  2018-01-31 14:16:35 2018-01-31 14:16:33 2018-01-31 14:14:13
## 4  2018-01-31 14:27:34 2018-01-31 13:56:49 2018-01-31 13:56:49
## 5  2018-01-31 14:27:34 2018-01-31 14:27:33 2018-01-31 14:27:33
## 6  2018-01-31 14:27:34 2018-01-31 14:27:34 2018-01-31 09:54:51
## 7  2018-01-31 14:27:34 2018-01-31 14:27:34 2018-01-31 09:54:51
## 8  2018-01-31 14:27:34 2018-01-31 14:27:34 2018-01-31 11:03:07
## 9  2018-01-31 13:46:08 2018-01-31 13:46:07 2018-01-31 13:46:07
## 10 2018-01-31 14:27:29 2018-01-31 14:24:24 2018-01-31 13:32:26
## 11 2018-01-31 14:22:58 2018-01-31 14:15:39 2018-01-31 14:15:39
## 12 2018-01-31 14:22:58 2018-01-31 14:22:58 2018-01-31 14:16:40
```

```r
## Sidebar: Why does Jenny name files this way? ----
library(tidyverse)
```

```
## ── Attaching packages ───────────────────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 2.2.1.9000     ✔ readr   1.1.1     
## ✔ tibble  1.4.2          ✔ dplyr   0.7.4     
## ✔ tidyr   0.8.0          ✔ stringr 1.2.0     
## ✔ ggplot2 2.2.1.9000     ✔ forcats 0.2.0
```

```
## ── Conflicts ──────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ tidyr::extract()   masks magrittr::extract()
## ✖ dplyr::filter()    masks stats::filter()
## ✖ dplyr::lag()       masks stats::lag()
## ✖ purrr::set_names() masks magrittr::set_names()
```

```r
ft <- tibble(files = dir_ls(glob = "*.R"))
ft
```

```
## # A tibble: 5 x 1
##   files                         
##   <fs::path>                    
## 1 00_filesystem-practice_comfy.R
## 2 00_filesystem-practice_jenny.R
## 3 01_explore-libraries_comfy.R  
## 4 01_explore-libraries_jenny.R  
## 5 01_explore-libraries_spartan.R
```

```r
ft %>%
  filter(str_detect(files, "explore"))
```

```
## # A tibble: 3 x 1
##   files                         
##   <fs::path>                    
## 1 01_explore-libraries_comfy.R  
## 2 01_explore-libraries_jenny.R  
## 3 01_explore-libraries_spartan.R
```

```r
ft %>%
  mutate(files = path_ext_remove(files)) %>%
  separate(files, into = c("i", "topic", "flavor"), sep = "_")
```

```
## # A tibble: 5 x 3
##   i     topic               flavor 
##   <chr> <chr>               <chr>  
## 1 00    filesystem-practice comfy  
## 2 00    filesystem-practice jenny  
## 3 01    explore-libraries   comfy  
## 4 01    explore-libraries   jenny  
## 5 01    explore-libraries   spartan
```

```r
dirs <- dir_ls(path_home("Desktop"), type = "directory")
(dt <- tibble(dirs = path_file(dirs)))
```

```
## # A tibble: 6 x 1
##   dirs                     
##   <fs::path>               
## 1 CCC PPT                  
## 2 CCF CRA 2018             
## 3 Eclipse Pics             
## 4 day1_s1_explore-libraries
## 5 day1_s2_copy-files       
## 6 explore-libraries
```

```r
dt %>%
  separate(dirs, into = c("day", "session", "topic"), sep = "_")
```

```
## Warning: Expected 3 pieces. Missing pieces filled with `NA` in 4 rows [1,
## 2, 3, 6].
```

```
## # A tibble: 6 x 3
##   day               session topic            
##   <chr>             <chr>   <chr>            
## 1 CCC PPT           <NA>    <NA>             
## 2 CCF CRA 2018      <NA>    <NA>             
## 3 Eclipse Pics      <NA>    <NA>             
## 4 day1              s1      explore-libraries
## 5 day1              s2      copy-files       
## 6 explore-libraries <NA>    <NA>
```

```r
## Principled use of delimiters --> meta-data can be recovered from filename

## Clean it out, so we reset for workshop ----
file_delete(to_files)
dir_ls()
```

```
## 00_filesystem-practice_comfy.R    00_filesystem-practice_comfy.html 
## 00_filesystem-practice_comfy.md   00_filesystem-practice_jenny.R    
## 00_filesystem-practice_jenny.Rmd  README.md                         
## explore-libraries.Rproj           scratch.Rmd                       
## scratch.html
```

