# Tile-collage
import numpy as np
import matplotlib.pyplot as plt
def mirror(img, axis):
  if axis == "x":
    return(img[::-1,:])
  elif axis == "y":
    return(img[:,::-1])
  elif axis == "xy": 
    return(img[::-1,::-1])
  
  
def remove_hue(img, hue):
  if hue == 'green':
    img[:,:,1] = 0
  elif hue == 'blue':
    img[:,:,2] = 0   
  elif hue == 'red':
    img[:,:,0] = 0   
  return(remove_hue)

def fourfold_tile(img):
  newimg = np.zeros((img.shape[0]*2,img.shape[1]*2,img.shape[2]))
  newimg[:img.shape[0],:img.shape[1]] = img 
  newimg[:img.shape[0],img.shape[1]:] = img  
  newimg[img.shape[0]:,:img.shape[1]] = img 
  newimg[img.shape[0]:,img.shape[1]:] = img 
  return(newimg)

def main():
  infile = input('Enter input file name: ')
  outFile = input('Enter output file name: ')
  img = plt.imread(infile)
  new_img = fourfold_tile(img)
  remove_hue(new_img[:img.shape[0],img.shape[1]:],'blue')
  remove_hue(new_img[img.shape[0]:,:img.shape[1]],'green')
  remove_hue(new_img[img.shape[0]:,img.shape[1]:],'red')
  new_img[:img.shape[0],img.shape[1]:] = mirror(new_img[:img.shape[0],img.shape[1]:],"y")
  new_img[img.shape[0]:,:img.shape[1]] = mirror(new_img[img.shape[0]:,:img.shape[1]],"x")
  new_img[img.shape[0]:,img.shape[1]:] = mirror(new_img[img.shape[0]:,img.shape[1]:],"xy")
  plt.imsave(outFile, new_img)

if __name__ == '__main__':
  main()
  
