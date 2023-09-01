---
title: Change Datatip to Custom Value in Matlab Plot
author: me
date: 2023-08-31 11:33:00 +0800
categories: [Blog, Matlab]
tags: [matlab]
pin: false
math: false
mermaid: false
---

# 🏁 Modified Datatip for Triangle Mesh

In Matlab plots you can use the datatip tool to receive the values at a plotted point. For example for a plot of a 3D triangle mesh this gives the `xyz` vertex positions:

![Desktop View](/assets/img/posts/datatip/nocustom.png){: width="300" height="auto" }

Especially for 3D shapes it might be more interesting to display the vertex _index_ rather than its coordinates as the vertex index is also used in the triangulation matrix. The desired datatip might then look as follows:

![Desktop View](/assets/img/posts/datatip/custom.png){: width="280" height="auto" }


# ✨ Matlab Code
To change the datatip we first want to create a file `changeDataTip2Idx.m` in which we put the following code. We basically just exchange the callback function called by the datatip for the current plot window. 
```matlab
function changeDataTip2Idx()
    dcm_obj = datacursormode(gcf);
    set(dcm_obj,'UpdateFcn',@callback)
    set(dcm_obj,'DisplayStyle','datatip','Enable','on')
end
```

Next up we need to specify the content of the callback function. This heavily relies on the data which is plotted:

```matlab
function output_txt = callback(obj, event_obj)
% Display the position of the data cursor
% obj          Currently not used (empty)
% event_obj    Handle to event object
% output_txt   Data cursor text string (string or cell array of strings).
    pos = get(event_obj, 'Position');

    % in my case there is a Vertices field available in the struct of the current plot
    VERTS = event_obj.Target.Vertices;

    % specify the new content which should be displayed
    output_txt = "create some nice string here";
end
```

# 🤓 Changing the Datatip for 3D Patches
With the following code inside a `changeDataTip2Idx.m` file a datatip for a `patch('Vertices', ..., 'Faces', ...)` plot can be achieved by executing the script via typing `changeDataTip2Idx()` into the matlab console _after_ plotting our 3D patch (make sure that no other plot window is selected).
```matlab
function changeDataTip2Idx()
    dcm_obj =datacursormode(gcf);
    set(dcm_obj,'UpdateFcn',@callback)
    set(dcm_obj,'DisplayStyle','datatip','Enable','on')
    
    
end

function output_txt = callback(obj, event_obj)
% Display the position of the data cursor
% obj          Currently not used (empty)
% event_obj    Handle to event object
% output_txt   Data cursor text string (string or cell array of strings).
    pos = get(event_obj,'Position');

    try
        VERTS = event_obj.Target.Vertices;
    catch
        VERTS = [event_obj.Target.XData', event_obj.Target.YData', event_obj.Target.ZData'];
    end

    output_txt = string(find(sum((VERTS - pos).^2, 2) == 0));
end
```

