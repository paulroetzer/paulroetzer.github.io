---
title: Generate Animated GIFs from Matlab Plot
author: Paul Roetzer
date: 2023-07-05 11:33:00 +0800
categories: [Blog, Matlab]
tags: [matlab]
pin: true
math: false
mermaid: false
---

# Generate animated GIFs from Plot Window

I recently had to create such an animation from a plot in matlab:

![Desktop View](/assets/img/posts/gif_from_plot/torusrot_nobounce.gif){: width="899" height="730" }

### 🐢 Prepare the animated plot
This code animates some data by rotating it around z-axis:
```
% M is a struct which contains vertices (M.VERT) and faces (M.TRIV) 
% mean center data
M.VERT = M.VERT - mean(unique(M.VERT));
% function to create rotationmatrix around z axis
rotmatZ = @(angle) [cos(angle) -sin(angle), 0; sin(angle), cos(angle), 0; 0 0 1];

angle_step = 0.01;
figure;
for i = 0:angle_step:2*pi
     % rotate data
     M.VERT  = M.VERT * rotmat(angle_step);
     % plot and delete
     patch('Faces', M.TRIV, 'Vertices', M.VERT, 'FaceColor', 'green'), axis equal, axis off
     view(3)
     xlim([-200, 200]), ylim([-200, 200]), zlim([-40, 40])
     drawnow
     delete(gca)
end
```

### 🌅 Export Gif
Gifs can be created in Matlab by using `exportgraphics(gca,"filename.gif", "Append",true)` (Note: the append options HAS to be true).
Unfortunately this might lead to some bouncy animation:
![Desktop View](/assets/img/posts/gif_from_plot/torusrot.gif){: width="500" height="400" }

This is due to some weird autoscaling (despite the manual axis limits we already set).
To overcome this, we can plot 4 points marking the boundary (these points will appear in the final gif but we can crop them with other software 🥴).
The final code looks as follows:

```matlab
angle_step = 0.01;
figure;
for i = 0:angle_step:2*pi
     % plot the extra points
     plot3([200, -200, -200, 200], [200, -200, 200, -200], [100, -100, 0, 0], '*')
     % rotate data
     M.VERT  = M.VERT * rotmat(angle_step);
     % plot and delete
     patch('Faces', M.TRIV, 'Vertices', M.VERT, 'FaceColor', 'green'), axis equal, axis off
     view(3)
     xlim([-200, 200]), ylim([-200, 200]), zlim([-40, 40])
     drawnow
     
     % export gif
     exportgraphics(gca,"torusrot.gif","Append",true)
     
     delete(gca)
end
```

