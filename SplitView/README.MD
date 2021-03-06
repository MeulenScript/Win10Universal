The SplitView control is a new addition to XAML for Windows 10 Applications. It’s basic use is to display a side menu, such as the one usually called “hamburger menu”.  One thing to note is that the SplitView is not a built in "Hamburger Menu".  It actually just gives you the ability to create a blank menu that you design and control.  In this sample, I created a simple hamburger menu that opens and closes by clicking the hamburger button.  I have also added a couple of "dummy" menu buttons that take no action.

The SplitView is quite straightforward to use.  You can think of it in terms of two different pieces, the Pane and the Content. The “Pane” property contains the code of the menu itself.  This would represent the different menu/navigation buttons in your app. The page content goes into the control itself.  Think of the content as the typical page you would have added to your application. 

<SplitView>
    <SplitView.Pane>    
      //Add your menu here
    </SplitView.Pane>
    <SplitView.Content>
      //Add your content here
    </SplitView.Content>
</SplitView>

A couple of properties to be familiar with...  
OpenPaneLength - The “OpenPaneLength” sets the width of the menu when it is open. 
PanePlacement - The “PanePlacement” property indicates on which side of the page the menu will appear (currently limited to left and right, top and bottom doesn’t seem to be supported). 
IsPaneOpen - The menu is opened by setting the “IsPaneOpen” property to true, and closed when the property is set to false or the user taps outside.  This can be changed dynamically from the code behind to open and close the menu, which is what we did in this sample.

DisplayMode - There are four different DisplayModes that you can choose from, Inline, Compay, Compact Overlay, Compact Inline
  Inline - When the menu pane is opened, it pushes the content over.  When it's closed, the content goes back to its original location
  Overlay - When the menu pane is opened, it lays on top of the content.  When it's closed, it is invisible.
  Compact Overlay - When the menu pane is opened, it pushes the content over.  When it's closed,the content goes back to its original position but the pane is still visible in Compact Mode.
  Compact Inline - When the menu pane is opened, it lays on top of the content.  When it's closed, the pane is still visible in Compact Mode.

<SplitView x:Name="MySplitView" DisplayMode="CompactOverlay"  IsPaneOpen="False" 
               CompactPaneLength="50" OpenPaneLength="150">
               
  As I mentioned earlier, the hamburger button is not actually built in, you have to create it.  To create a Hamburger Button we are going to use the Segoe MDL2 Assets font and use the code "&#xE700;" like this.
  
  <Button x:Name="HamburgerButton" FontFamily="Segoe MDL2 Assets" Content="&#xE700;"
                    Width="50" Height="50" Background="Transparent" Click="HamburgerButton_Click"/>
  For adding additional menu buttons, I added a stackpanel and created extra buttons similar to the HamburgerButton.  I simply named them differently and gave them a different icon.
  
              <StackPanel Background="Gray">
                <Button x:Name="HamburgerButton" FontFamily="Segoe MDL2 Assets" Content="&#xE700;"
                    Width="50" Height="50" Background="Transparent" Click="HamburgerButton_Click"/>
                <StackPanel Orientation="Horizontal">
                    <Button x:Name="MenuButton1" FontFamily="Segoe MDL2 Assets" Content="&#xE825;"
                    Width="50" Height="50" Background="Transparent"/>
                    <TextBlock Text="Button 1" FontSize="18" VerticalAlignment="Center" />
                </StackPanel>
                <StackPanel Orientation="Horizontal">
                    <Button x:Name="MenuButton2" FontFamily="Segoe MDL2 Assets" Content="&#xE10F;"
                        Width="50" Height="50" Background="Transparent"/>
                    <TextBlock Text="Button 2" FontSize="18" VerticalAlignment="Center" />
                </StackPanel>
                <StackPanel Orientation="Horizontal">
                    <Button x:Name="MenuButton3" FontFamily="Segoe MDL2 Assets" Content="&#xE1D6;"
                        Width="50" Height="50" Background="Transparent"/>
                    <TextBlock Text="Button 3" FontSize="18" VerticalAlignment="Center" />
              </StackPanel>
                
  
  For my content, I just have a Textblock.
  
       <SplitView.Content>
            <Grid>
              <TextBlock Text="SplitView Basic" FontSize="54" Foreground="White"
                           HorizontalAlignment="Center" VerticalAlignment="Center"/>
            </Grid>
        </SplitView.Content>
        
The last step is to add the Click Handler for our Hamburger Button to open and close the menu pane.

private void HamburgerButton_Click(object sender, RoutedEventArgs e)
		{
			MySplitView.IsPaneOpen = !MySplitView.IsPaneOpen;
		}
