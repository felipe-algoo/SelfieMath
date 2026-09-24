
- Your phone's camera doesn't capture RGB pixels the way you'd think. Instead, it uses a Bayer pattern sensor where each photosite only sees one color through a microscopic filter array. 
***Red at position (0,0), green at (0,1), green at (1,0), blue at (1,1)***, repeating across millions of sites. The chip literally samples color at half or quarter resolution depending on the channel.
  
- Demosaicing algorithms then interpolate the missing values. I'm using bilinear interpolation in this demo, though production cameras run far more sophisticated edge-aware methods to prevent color artifacts near sharp transitions. 

- The math here involves weighted averaging of neighboring pixels based on their spatial relationships, essentially solving for unknown values in a sparse 2D color field.
  
- Gamma correction comes next, which corrects for the nonlinear relationship between voltage and perceived brightness. Cameras apply an inverse gamma ***(typically γ=2.2)*** to encode linear sensor values into perceptual space. 

- Without this, your image would look washed out because human vision perceives intensity logarithmically rather than linearly. The transform is simple but critical: $L_\text{out}= L_\text{in}^{\frac{1}{\gamma}}$
  
- The sensor can't capture full color, so we interpolate. Light response isn't linear, so we apply gamma. Colors shift with illumination, so we balance. Our eyes prefer enhanced edges, so we sharpen. 

- The selfie you see is actually a heavily processed mathematical reconstruction, optimized for human visual preference rather than physical accuracy.


<img width="567" height="590" alt="img" src="https://github.com/user-attachments/assets/1edbff53-2644-4651-92df-ed66c0c644e7" />
