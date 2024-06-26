---
type: rule
title: Do your Windows Forms have border protection?
uri: do-your-windows-forms-have-border-protection
authors:
  - title: Adam Cogan
    url: https://ssw.com.au/people/adam-cogan
related: []
redirects: []
created: 2014-12-01T01:03:09.000Z
archivedreason: null
guid: 51a95539-4424-4b7a-aa1e-4af0d72f5127
---

Border protection helps us design Windows Forms properly without placing controls too near to the border. Maintain a consistent alignment makes the Windows Forms look better, especially on designing wizard forms  where all forms have the same size.

<!--endintro-->

::: good  
![Figure: Good example - Good border protection on a form at run time. The only problem is you would have to imagine these blue lines to get consistency](../../assets/BorderProtectionExample.gif)  
:::

**Border protection in action:**

::: bad  
![Figure: Bad example - Controls placed very near to the border and not aligned correctly](../../assets/BorderProtectionBad.gif)  
:::

::: good  
![Figure: Good example - All controls are in the border protection area and aligned correctly](../../assets/BorderProtectionGood.gif)  
:::

![Figure: Design mode](../../assets/BorderProtectionDesign.gif)  

The way to implement border protection (the 2 vertical red lines) is implement it in the base form or base user control, and all other forms and user controls inherit the base class to get consistent border protection lines.

```csharp
private void BaseForm_Paint(object sender, PaintEventArgs e)
            {
                // Draw border protection lines 
                if (this.DesignMode) 
                { 
                   Pen pen = new Pen(Color.Red); 
                   e.Graphics.DrawLine(pen,
                            23, 0, 23, this.Height); 
                            e.Graphics.DrawLine(pen, this.Width - 23, 0, this.Width - 23, this.Height); 
                } 
            }
```

#### Q&A

**Why don't we put a panel on the form and set the form DockPadding property which does a similar thing?** 

* Adding more panels docking to a form reduces the performance significantly because of the extra SuspendLayout and ResumeLayout calls.
* In certain cases we might really want a control to stick at the border, if we use DockPadding Property, we can't make any exceptions. And still, these red lines actually just act like a ruler to help us easily see whether the controls are aligned nicely.
