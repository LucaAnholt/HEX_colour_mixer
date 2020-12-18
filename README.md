# multi_hex_mix
Description:
R code for mixing multiple hex codes - particularly useful in colouring edges in connected networks/graphs to visualise/demonstrate overlap. 

How to use:
Arguments: 
col_vector = the vector of hex codes you wish to mix 

Example: 
#loading libraries:
library(colorspace)
library(grDevices)

#creating a vector of hex codes: 
col <- c("#8376ca",
         "#9b9d3f",
         "#c9578f",
         "#50ac72",
         "#c96840")

#running function: 
multi_hex_col_mix <- function(col_vector){
  rgb <- as.vector(col2rgb(col_vector))
  rgb <- as.data.frame(matrix(rgb, ncol = 3,  byrow = TRUE), stringsAsFactors = FALSE)
  
  
  mix <- mixcolor(0.5, RGB(R = rgb$V1[1], G = rgb$V2[1], B = rgb$V3[1]), RGB(R = rgb$V1[2], G = rgb$V2[2], B = rgb$V3[2]))
  count <- as.numeric(seq(1, length(rgb$V1))[-c(1,2)])
  for(i in count){
    mix <- mixcolor(0.5, mix, RGB(R = rgb$V1[i], G = rgb$V2[i], B = rgb$V3[i]))
  }
  
  mix <- c(mix@coords[1], mix@coords[2], mix@coords[3])
  mix <- unique(rgb(red = mix[1], green = mix[2], blue = mix[3], maxColorValue = 255))
  return(mix)
}

#running function:
multi_hex_col_mix(col_vector = col)
