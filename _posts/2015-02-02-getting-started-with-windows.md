# Getting Started With Windows

I'll present a recommended setup for getting started with BowTie.io development
on the Windows platform. There are a number of other methods, including the
GitHub Windows client, but these may require additional work or more intensive
configuration.

Some existing software solutions that BowTie.io integrates with do not officially
support Windows, but we've found that there's not much hindrance to development
once you've configured your environment. Please reach out to help@bowtie.io if
you have any issues, or submit a Pull Request to submit any corrections.

## Installing Git

1. Download the official Git build for Windows from the [GitHub Downloads
   Page](http://www.git-scm.com/download/win).
1. Run the executable file that you just downloaded to begin the Git
   installation process.
1. Install with the defaut options (esp. Use Git from Git Bash only).

## Configuring SSH Keys

1. Click the Start Button, find the `Git Bash` Application, and run it.
1. In the resulting terminal window, run `$ ssh-keygen.exe`
1. Save the file the default location (%HOMEDIR%/.ssh/id_rsa).
1. Now run `$ cat %HOMEDIR%/.ssh/id_rsa.pub | clip`, where %HOMEDIR% should be
   your user's home directory
1. Navigate to the [BowTie.io New Account Key](https://bowtie.io/keys/new) page
   and paste the clipboard contents into the "Key" field.
1. Give your Key a Title that describes the machine you're working from, and
   submit with the "Save" button.

## Cloning the Repository

1. Visit your BowTie.io Project Dashboard, and copy the value from the "SSH
   clone URL" field at the top of the page.
1. Launch the `Git Bash` Application and navigate to the directory where you
   want your Projects to live.
1. Run `$ git clone %GITCLONEURL%`, where `%GITCLONEURL%` is the value from the
   "SSH clone URL" field from step 1.
1. If your configuration is correct, you should see Git pull down your Project
   contents into a directory named after your Project.

## Installing Ruby

1. Download Ruby (2.1.5 works, as of the date of this writing) from
   [RubyInstaller](http://rubyinstaller.org/downloads/).
1. Run the Installer - make sure you "Add Ruby executables to your PATH"
1. Download the DevKit release for the same version of Ruby you downloaded
   above.
1. Extract the DevKit release into `C:\RubyDevKit`
1. Run the Command Prompt with Ruby from your start menu
1. Run `cd \RubyDevKit`
1. Run `$ ruby dk.rb init`
1. Run `$ ruby dk.rb install`
1. Run `$ gem update` and confirm overwrites

## The BowTie Client

1. Run `gem install bowtie-io` and accept any Security Prompts.
1. In your Project's clone directory, edit the `_config.yml` file and add the
   line `highlighter: false`. Without it you'll get blank pages served. If you
   figure out how to get pygments working on Windows, please let us know.
1. Run `$ bowtie serve` and open http://localhost:4000/ in your web browser.
