# Inspect clipboard with linqpad

While testing the upcoming NimbleText enhancements I need to be able to inspect the line endings on the clipboard, so put this linqpad script into my [linqpad script folder](invoke_linqpad_commandlet.md)

![inspect_clipboard_1.png](inspect_clipboard_1.png)

now if i type `linq inspect_clipboard` I will instantly see, color coded, what special characters are in the clipboard.

![inspect_clipboard_2.png](inspect_clipboard_2.png)


Code (requires a reference and Additional namespace import of `System.Windows.Forms` (hit F4)

    void Main()
    {
        var text = Clipboard.GetText();
        foreach(var c in text) 
        {
            switch(c)
            {
                case '\t' : WriteColor("\\t", ConsoleColor.Yellow); break;
                case '\r' : WriteColor("\\r", ConsoleColor.Yellow);	break;
                case '\n' : WriteColor("\\t", ConsoleColor.Yellow);	Console.WriteLine(); break; 
                default:	Console.Write(c); break;
            }		
        }
    }

    void WriteColor(string text, ConsoleColor color) {
        Console.ForegroundColor = color;
        Console.Write(text);
        Console.ResetColor();
    }
    