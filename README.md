# Autoscrolling-TextEdit-QML



Note that the TextEdit does not implement scrolling, 
following the cursor, or other behaviors specific to a look-and-feel. 
For example, to add flickable scrolling that follows the cursor:

QML:
```
Flickable {
     id: flick

     width: 300; height: 200;
     contentWidth: edit.paintedWidth
     contentHeight: edit.paintedHeight
     clip: true

     function ensureVisible(r)
     {
         if (contentX >= r.x)
             contentX = r.x;
         else if (contentX+width <= r.x+r.width)
             contentX = r.x+r.width-width;
         if (contentY >= r.y)
             contentY = r.y;
         else if (contentY+height <= r.y+r.height)
             contentY = r.y+r.height-height;
     }

     TextEdit {
         id: edit
         width: flick.width
         height: flick.height
         focus: true
         wrapMode: TextEdit.Wrap
         onCursorRectangleChanged: flick.ensureVisible(cursorRectangle)
     }
 }
```

Credit: https://gist.github.com/tstellanova/a34ba9553c0ade00824a4e071d9abe56 
