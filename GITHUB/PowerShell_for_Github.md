# PowerShellforGithub
In some circumstances, you may wish to use github via PowerShell such as in an Azure runbook where
the `$git` command may not be available.

* Install from: https://www.powershellgallery.com/packages/PowerShellForGitHub/
* Source code: https://github.com/Microsoft/PowerShellForGitHub

| Cmdlet | Synopsis |
| --- | --- |
| [Delete-GitHubComment (Alias)](#delete-githubcomment-alias) |  |
| [Delete-GitHubLabel (Alias)](#delete-githublabel-alias) |  |
| [Delete-GitHubMilestone (Alias)](#delete-githubmilestone-alias) |  |
| [Delete-GitHubRepository (Alias)](#delete-githubrepository-alias) | Removes/deletes a repository from GitHub. |
| [Get-GitHubBranch (Alias)](#get-githubbranch-alias) | Retrieve branches for a given GitHub repository. |
| [Transfer-GitHubRepositoryOwnership (Alias)](#transfer-githubrepositoryownership-alias) | Creates a new repository on GitHub. |
| [Add-GitHubIssueLabel](#add-githubissuelabel) |  |
| [Backup-GitHubConfiguration](#backup-githubconfiguration) | Exports the user's current configuration file. |
| [Clear-GitHubAuthentication](#clear-githubauthentication) | Clears out any GitHub API token from memory, as well as from local file storage. |
| [ConvertFrom-GitHubMarkdown](#convertfrom-githubmarkdown) | Converts arbitrary Markdown into HTML. |
| [Get-GitHubAssignee](#get-githubassignee) |  |
| [Get-GitHubCloneTraffic](#get-githubclonetraffic) | Get the total number of clones and breakdown per day or week for the last 14 days for the given Github Repository. |
| [Get-GitHubCodeOfConduct](#get-githubcodeofconduct) | Gets license or license content from GitHub. |
| [Get-GitHubComment](#get-githubcomment) |  |
| [Get-GitHubConfiguration](#get-githubconfiguration) | Gets the currently configured value for the requested configuration setting. |
| [Get-GitHubEmoji](#get-githubemoji) | Gets all the emojis available to use on GitHub. |
| [Get-GitHubEvent](#get-githubevent) |  |
| [Get-GitHubGitIgnore](#get-githubgitignore) | Gets the list of available .gitignore templates, or their content, from GitHub. |
| [Get-GitHubIssue](#get-githubissue) | Retrieve Issues from GitHub. |
| [Get-GitHubIssueTimeline](#get-githubissuetimeline) | Retrieves various events that occur around an issue or pull request on GitHub. |
| [Get-GitHubLabel](#get-githublabel) | Retrieve label(s) of a given GitHub repository. |
| [Get-GitHubLicense](#get-githublicense) | Gets a license list or license content from GitHub. |
| [Get-GitHubMilestone](#get-githubmilestone) |  |
| [Get-GitHubOrganizationMember](#get-githuborganizationmember) | Retrieve list of members within an organization. |
| [Get-GitHubPathTraffic](#get-githubpathtraffic) | Get the top 10 popular contents over the last 14 days for a given Github repository. |
| [Get-GitHubPullRequest](#get-githubpullrequest) | Retrieve the pull requests in the specified repository. |
| [Get-GitHubRateLimit](#get-githubratelimit) | Gets the current rate limit status for the GitHub API based on the currently configuredauthentication (Access Token). |
| [Get-GitHubReferrerTraffic](#get-githubreferrertraffic) | Get the top 10 referrers over the last 14 days for a given GitHub repository. |
| [Get-GitHubRepository](#get-githubrepository) | Retrieves information about a repository or list of repoistories on GitHub. |
| [Get-GitHubRepositoryBranch](#get-githubrepositorybranch) | Retrieve branches for a given GitHub repository. |
| [Get-GitHubRepositoryCollaborator](#get-githubrepositorycollaborator) | Retrieve list of contributors for a given repository. |
| [Get-GitHubRepositoryContributor](#get-githubrepositorycontributor) | Retrieve list of contributors for a given repository. |
| [Get-GitHubRepositoryFork](#get-githubrepositoryfork) | Gets the list of forks of the specified repository on GitHub. |
| [Get-GitHubRepositoryLanguage](#get-githubrepositorylanguage) | Retrieves a list of the programming languages used in a repository on GitHub. |
| [Get-GitHubRepositoryTag](#get-githubrepositorytag) | Retrieves tags for a repository on GitHub. |
| [Get-GitHubRepositoryTopic](#get-githubrepositorytopic) | Retrieves information about a repository on GitHub. |
| [Get-GitHubTeam](#get-githubteam) | Retrieve a team or teams within an organization or repository on GitHub. |
| [Get-GitHubTeamMember](#get-githubteammember) | Retrieve list of team members within an organization. |
| [Get-GitHubUser](#get-githubuser) | Retrieves information about the specified user on GitHub. |
| [Get-GitHubUserContextualInformation](#get-githubusercontextualinformation) | Retrieves contextual information about the specified user on GitHub. |
| [Get-GitHubViewTraffic](#get-githubviewtraffic) | Get the total number of views and breakdown per day or week for the last 14 days for the given Github Repository. |
| [Group-GitHubIssue](#group-githubissue) | Groups the provided issues based on the specified grouping criteria. |
| [Invoke-GHRestMethod](#invoke-ghrestmethod) | A wrapper around Invoke-WebRequest that understands the Store API. |
| [Invoke-GHRestMethodMultipleResult](#invoke-ghrestmethodmultipleresult) | A special-case wrapper around Invoke-GHRestMethod that understands GET URI'swhich support the 'top' and 'max' parameters. |
| [Lock-GitHubIssue](#lock-githubissue) | Lock an Issue or Pull Request conversation on GitHub. |
| [Move-GitHubRepositoryOwnership](#move-githubrepositoryownership) | Creates a new repository on GitHub. |
| [New-GithubAssignee](#new-githubassignee) |  |
| [New-GitHubComment](#new-githubcomment) |  |
| [New-GitHubIssue](#new-githubissue) | Create a new Issue on GitHub. |
| [New-GitHubLabel](#new-githublabel) | Create a new label on a given GitHub repository. |
| [New-GitHubMilestone](#new-githubmilestone) |  |
| [New-GitHubRepository](#new-githubrepository) | Creates a new repository on GitHub. |
| [New-GitHubRepositoryFork](#new-githubrepositoryfork) | Creates a new fork of a repository on GitHub. |
| [Remove-GithubAssignee](#remove-githubassignee) |  |
| [Remove-GitHubComment](#remove-githubcomment) |  |
| [Remove-GitHubIssueLabel](#remove-githubissuelabel) |  |
| [Remove-GitHubLabel](#remove-githublabel) | Deletes a label from a given GitHub repository. |
| [Remove-GitHubMilestone](#remove-githubmilestone) |  |
| [Remove-GitHubRepository](#remove-githubrepository) | Removes/deletes a repository from GitHub. |
| [Reset-GitHubConfiguration](#reset-githubconfiguration) | Clears out the user's configuration file and configures this session with all defaultconfiguration values. |
| [Restore-GitHubConfiguration](#restore-githubconfiguration) | Sets the specified file to be the user's configuration file. |
| [Set-GitHubAuthentication](#set-githubauthentication) | Allows the user to configure the API token that should be used for authenticationwith the GitHub API. |
| [Set-GitHubComment](#set-githubcomment) |  |
| [Set-GitHubConfiguration](#set-githubconfiguration) | Change the value of a configuration property for the PowerShellForGitHub module,for the sesion only, or globally for this user. |
| [Set-GitHubIssueLabel](#set-githubissuelabel) |  |
| [Set-GitHubLabel](#set-githublabel) | Sets the entire set of Labels on the given GitHub repository to match the provided listof Labels. |
| [Set-GitHubMilestone](#set-githubmilestone) |  |
| [Set-GitHubRepositoryTopic](#set-githubrepositorytopic) | Replaces all topics for a repository on GitHub. |
| [Split-GitHubUri](#split-githuburi) | Extracts the relevant elements of a GitHub repository Uri and returns the requested element. |
| [Test-GitHubAssignee](#test-githubassignee) |  |
| [Test-GitHubAuthenticationConfigured](#test-githubauthenticationconfigured) | Indicates if a GitHub API Token has been configured for this module via Set-GitHubAuthentication. |
| [Test-GitHubOrganizationMember](#test-githuborganizationmember) | Check to see if a user is a member of an organization. |
| [Unlock-GitHubIssue](#unlock-githubissue) | Unlocks an Issue or Pull Request conversation on GitHub. |
| [Update-GitHubCurrentUser](#update-githubcurrentuser) | Updates information about the current authenticated user on GitHub. |
| [Update-GitHubIssue](#update-githubissue) | Create a new Issue on GitHub. |
| [Update-GitHubLabel](#update-githublabel) | Updates an existing label on a given GitHub repository. |
| [Update-GitHubRepository](#update-githubrepository) | Updates the details of an existing repository on GitHub. |

---
## Delete-GitHubComment (Alias)

### Synopsis



### Syntax

Remove-GitHubComment [-OwnerName <String>] [-RepositoryName <String>] -CommentID <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubComment -Uri <String> -CommentID <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a Github comment for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-CommentID <String>
	    The id of the comment to delete.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubComment -OwnerName Microsoft -RepositoryName PowerShellForGitHub -CommentID 1

Deletes a Github comment from the Microsoft\PowerShellForGitHub project.

---
## Delete-GitHubLabel (Alias)

### Synopsis



### Syntax

Remove-GitHubIssueLabel -OwnerName <String> -RepositoryName <String> -Issue <Int64> [-Name <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubIssueLabel -Uri <String> -Issue <Int64> [-Name <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a label from an issue in the given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to remove the label from.

	-Name <String>
	    Name of the label to be deleted. If not provided, will delete all labels on the issue.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubIssueLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Name TestLabel -Issue 1

Removes the label called "TestLabel" from issue 1 in the PowerShellForGitHub project.

---
## Delete-GitHubMilestone (Alias)

### Synopsis



### Syntax

Remove-GitHubMilestone -OwnerName <String> -RepositoryName <String> -Milestone <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubMilestone -Uri <String> -Milestone <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a Github milestone for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Milestone <String>
	    The number of a specific milestone to delete.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubMilestone -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Milestone 1

Deletes a Github milestone from the Microsoft\PowerShellForGitHub project.

---
## Delete-GitHubRepository (Alias)

### Synopsis

Removes/deletes a repository from GitHub.

### Syntax

Remove-GitHubRepository [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubRepository -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Removes/deletes a repository from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubRepository -OwnerName You -RepositoryName YourRepoToDelete






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Remove-GitHubRepository -Uri https://github.com/You/YourRepoToDelete

---
## Get-GitHubBranch (Alias)

### Synopsis

Retrieve branches for a given GitHub repository.

### Syntax

Get-GitHubRepositoryBranch [-OwnerName <String>] [-RepositoryName <String>] [-Name <String>] [-ProtectedOnly] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryBranch -Uri <String> [-Name <String>] [-ProtectedOnly] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve branches for a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Name of the specific branch to be retieved.  If not supplied, all branches will be retrieved.

	-ProtectedOnly <SwitchParameter>

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryBranch -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets all branches for the specified repository.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryBranch -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -Name master

Gets information only on the master branch for the specified repository.

---
## Transfer-GitHubRepositoryOwnership (Alias)

### Synopsis

Creates a new repository on GitHub.

### Syntax

Move-GitHubRepositoryOwnership [-OwnerName <String>] [-RepositoryName <String>] -NewOwnerName <String> [-TeamId <Int64[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

Move-GitHubRepositoryOwnership -Uri <String> -NewOwnerName <String> [-TeamId <Int64[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-NewOwnerName <String>
	    The username or organization name the repository will be transferred to.

	-TeamId <Int64[]>
	    ID of the team or teams to add to the repository.  Teams can only be added to
	    organization-owned repositories.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Move-GitHubRepositoryOwnership -OwnerName Microsoft -RepositoryName PowerShellForGitHub -NewOwnerName OctoCat

---
## Add-GitHubIssueLabel

### Synopsis



### Syntax

Add-GitHubIssueLabel -OwnerName <String> -RepositoryName <String> -Issue <Int64> -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Add-GitHubIssueLabel -Uri <String> -Issue <Int64> -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Adds a label to an issue in the given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to add the label to.

	-Name <String[]>
	    Array of label names to add to the issue

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Add-GitHubIssueLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 1 -Name $labels

Adds labels to an issue in the PowerShellForGitHub project.

---
## Backup-GitHubConfiguration

### Synopsis

Exports the user's current configuration file.

### Syntax

Backup-GitHubConfiguration [[-Path] <String>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Exports the user's current configuration file.

This is primarily used for unit testing scenarios.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Path <String>
	    The path to store the user's current configuration file.

	-Force <SwitchParameter>
	    If specified, will overwrite the contents of any file with the same name at th
	    location specified by Path.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Backup-GitHubConfiguration -Path 'c:\foo\config.json'

Writes the user's current configuration file to c:\foo\config.json.

---
## Clear-GitHubAuthentication

### Synopsis

Clears out any GitHub API token from memory, as well as from local file storage.

### Syntax

Clear-GitHubAuthentication [-SessionOnly] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Clears out any GitHub API token from memory, as well as from local file storage.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-SessionOnly <SwitchParameter>
	    By default, this will clear out the cache in memory, as well as in the local
	    configuration file.  If this switch is specified, authentication will be cleared out
	    in this session only -- the local configuration file cache will remain
	    (and thus still be available in a new PowerShell session).

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Clear-GitHubAuthentication

Clears out any GitHub API token from memory, as well as from local file storage.

---
## ConvertFrom-GitHubMarkdown

### Synopsis

Converts arbitrary Markdown into HTML.

### Syntax

ConvertFrom-GitHubMarkdown [-Content] <String> [[-Mode] <String>] [[-Context] <String>] [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Converts arbitrary Markdown into HTML.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Content <String>
	    The Markdown text to render to HTML.  Content must be 400 KB or less.

	-Mode <String>
	    The rendering mode for the Markdown content.
	    
	    Markdown - Renders Content in plain Markdown, just like README.md files are rendered
	    
	    GitHubFlavoredMarkdown - Creates links for user mentions as well as references to
	    SHA-1 hashes, issues, and pull requests.

	-Context <String>
	    The repository to use when creating references in 'githubFlavoredMarkdown' mode.
	    Specify as [ownerName]/[repositoryName].

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>ConvertFrom-GitHubMarkdown -Content '**Bolded Text**' -Mode Markdown

Returns back '<p><strong>Bolded Text</strong></p>'

---
## Get-GitHubAssignee

### Synopsis



### Syntax

Get-GitHubAssignee [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubAssignee -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Lists the available assignees for issues in a repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubAsigneeList -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Lists the available assignees for issues from the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubCloneTraffic

### Synopsis

Get the total number of clones and breakdown per day or week for the last 14 days for the given Github Repository.

### Syntax

Get-GitHubCloneTraffic [-OwnerName <String>] [-RepositoryName <String>] [-Per <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubCloneTraffic -Uri <String> [-Per <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Get the total number of clones and breakdown per day or week for the last 14 days.
Timestamps are aligned to UTC midnight of the beginning of the day or week. Week begins on Monday.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Per <String>
	    The interval at which return to return the view counts.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubCloneTraffic -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the total number of clones and breakdown per day or week for the last 14 days from the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubCodeOfConduct

### Synopsis

Gets license or license content from GitHub.

### Syntax

Get-GitHubCodeOfConduct [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubCodeOfConduct -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubCodeOfConduct -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets license or license content from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    The name of the license to retrieve the content for.  If not specified, all licenses
	    will be returned.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubCodeOfConduct

Returns metadata about popular Codes of Conduct




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubCodeOfConduct -Name citizen_code_of_conduct

Gets the content of the 'Citizen Code of Conduct'




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Get-GitHubCodeOfConduct -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets the content of the Code of Coduct file for the Microsoft\PowerShellForGitHub repository
if one is detected.

It may be necessary to convert the content of the file.  Check the 'encoding' property of
the result to know how 'content' is encoded.  As an example, to convert from Base64, do
the following:

[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($result.content))

---
## Get-GitHubComment

### Synopsis



### Syntax

Get-GitHubComment -OwnerName <String> -RepositoryName <String> [-Since <DateTime>] [-Sort <String>] [-Direction <String>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] 
[-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubComment -OwnerName <String> -RepositoryName <String> -CommentID <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubComment -OwnerName <String> -RepositoryName <String> -Issue <Int64> [-Since <DateTime>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

Get-GitHubComment -Uri <String> -CommentID <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubComment -Uri <String> -Issue <Int64> [-Since <DateTime>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubComment -Uri <String> [-Since <DateTime>] [-Sort <String>] [-Direction <String>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

### Description

Get the comments for a given Github repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-CommentID <String>
	    The ID of a specific comment to get. If not supplied, will return back all comments for this repository.

	-Issue <Int64>
	    Issue number to get comments for. If not supplied, will return back all comments for this repository.

	-Since <DateTime>
	    Only comments updated at or after this time are returned.

	-Sort <String>
	    How to sort the results.

	-Direction <String>
	    How to list the results. Ignored without the sort parameter.

	-MediaType <String>
	    The format in which the API will return the body of the comment.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubComment-OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the comments for the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubConfiguration

### Synopsis

Gets the currently configured value for the requested configuration setting.

### Syntax

Get-GitHubConfiguration [-Name] <String> [<CommonParameters>]

### Description

Gets the currently configured value for the requested configuration setting.

Always returns the value for this session, which may or may not be the persisted
setting (that all depends on whether or not the setting was previously modified
during this session using Set-GitHubConfiguration -SessionOnly).

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Name <String>
	    The name of the configuration whose value is desired.

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubConfiguration -Name WebRequestTimeoutSec

Gets the currently configured value for WebRequestTimeoutSec for this PowerShell session
(which may or may not be the same as the persisted configuration value, depending on
whether this value was modified during this session with Set-GitHubConfiguration -SessionOnly).

---
## Get-GitHubEmoji

### Synopsis

Gets all the emojis available to use on GitHub.

### Syntax

Get-GitHubEmoji [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets all the emojis available to use on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubEmoji

---
## Get-GitHubEvent

### Synopsis



### Syntax

Get-GitHubEvent -OwnerName <String> -RepositoryName <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubEvent -OwnerName <String> -RepositoryName <String> -EventID <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubEvent -OwnerName <String> -RepositoryName <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubEvent -Uri <String> -EventID <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubEvent -Uri <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubEvent -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Lists events for an issue, repository, or a single event

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-EventID <Int64>
	    The ID of a specific event to get. If not supplied, will return back all events for this repository.

	-Issue <Int64>
	    Issue number to get events for. If not supplied, will return back all events for this repository.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubEvent -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the events for the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubGitIgnore

### Synopsis

Gets the list of available .gitignore templates, or their content, from GitHub.

### Syntax

Get-GitHubGitIgnore [[-Name] <String>] [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets the list of available .gitignore templates, or their content, from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Name <String>
	    The name of the .gitignore template whose content should be fetched.
	    Not providing this will cause a list of all available templates to be returned.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubGitIgnore

Returns the list of all available .gitignore templates.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubGitIgnore -Name VisualStudio

Returns the content of the VisualStudio.gitignore template.

---
## Get-GitHubIssue

### Synopsis

Retrieve Issues from GitHub.

### Syntax

Get-GitHubIssue [-OwnerName <String>] [-RepositoryName <String>] [-OrganizationName <String>] [-RepositoryType <String>] [-Issue <Int64>] [-IgnorePullRequests] [-Filter <String>] [-State 
<String>] [-Label <String[]>] [-Sort <String>] [-Direction <String>] [-Since <DateTime>] [-MilestoneType <String>] [-Milestone <String>] [-AssigneeType <String>] [-Assignee <String>] 
[-Creator <String>] [-Mentioned <String>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubIssue -Uri <String> [-OrganizationName <String>] [-RepositoryType <String>] [-Issue <Int64>] [-IgnorePullRequests] [-Filter <String>] [-State <String>] [-Label <String[]>] [-Sort 
<String>] [-Direction <String>] [-Since <DateTime>] [-MilestoneType <String>] [-Milestone <String>] [-AssigneeType <String>] [-Assignee <String>] [-Creator <String>] [-Mentioned <String>] 
[-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve Issues from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-OrganizationName <String>
	    The organization whose issues should be retrieved.

	-RepositoryType <String>
	    all: Retrieve issues  across owned, member and org repositories
	    ownedAndMember: Retrieve issues across owned and member repositories

	-Issue <Int64>
	    The number of specic Issue to retrieve.  If not supplied, will return back all
	    Issues for this Repository that match the specified criteria.

	-IgnorePullRequests <SwitchParameter>
	    GitHub treats Pull Requests as Issues.  Specify this switch to skip over any
	    Issue that is actually a Pull Request.

	-Filter <String>
	    Indicates the type of Issues to return:
	    assigned: Issues assigned to the authenticated user.
	    created: Issues created by the authenticated user.
	    mentioned: Issues mentioning the authenticated user.
	    subscribed: Issues the authenticated user has been subscribed to updates for.
	    all: All issues the authenticated user can see, regardless of participation or creation.

	-State <String>
	    Indicates the state of the issues to return.

	-Label <String[]>
	    The label (or labels) that returned Issues should have.

	-Sort <String>
	    The property to sort the returned Issues by.

	-Direction <String>
	    The direction of the sort.

	-Since <DateTime>
	    If specified, returns only issues updated at or after this time.

	-MilestoneType <String>
	    If specified, indicates what milestone Issues must be a part of to be returned:
	      specific: Only issues with the milestone specified via the Milestone parameter will be returned.
	      all: All milestones will be returned.
	      none: Only issues without milestones will be returned.

	-Milestone <String>
	    Only issues with this milestone will be returned.

	-AssigneeType <String>
	    If specified, indicates who Issues must be assigned to in order to be returned:
	      specific: Only issues assigned to the user specified by the Assignee parameter will be returned.
	      all: Issues assigned to any user will be returned.
	      none: Only issues without an assigned user will be returned.

	-Assignee <String>
	    Only issues assigned to this user will be returned.

	-Creator <String>
	    Only issues created by this specified user will be returned.

	-Mentioned <String>
	    Only issues that mention this specified user will be returned.

	-MediaType <String>
	    The format in which the API will return the body of the issue.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -State Open

Gets all the currently open issues in the Microsoft\PowerShellForGitHub repository.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -State All -Assignee Octocat

Gets every issue in the Microsoft\PowerShellForGitHub repository that is assigned to Octocat.

---
## Get-GitHubIssueTimeline

### Synopsis

Retrieves various events that occur around an issue or pull request on GitHub.

### Syntax

Get-GitHubIssueTimeline [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubIssueTimeline -Uri <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves various events that occur around an issue or pull request on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    The Issue to get the timeline for.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubIssueTimeline -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 24

---
## Get-GitHubLabel

### Synopsis

Retrieve label(s) of a given GitHub repository.

### Syntax

Get-GitHubLabel -OwnerName <String> -RepositoryName <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -OwnerName <String> -RepositoryName <String> -Milestone <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -OwnerName <String> -RepositoryName <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -OwnerName <String> -RepositoryName <String> -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -Uri <String> -Milestone <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -Uri <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -Uri <String> -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLabel -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve label(s) of a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Name of the specific label to be retieved.  If not supplied, all labels will be retrieved.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-Issue <Int64>
	    If provided, will return all of the labels for this particular issue.

	-Milestone <Int64>
	    If provided, will return all of the labels for this particular milestone.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets the information for every label from the Microsoft\PowerShellForGitHub project.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -LabelName TestLabel

Gets the information for the label named "TestLabel" from the Microsoft\PowerShellForGitHub
project.

---
## Get-GitHubLicense

### Synopsis

Gets a license list or license content from GitHub.

### Syntax

Get-GitHubLicense [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLicense -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubLicense -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets a license list or license content from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    The name of the license to retrieve the content for.  If not specified, all licenses
	    will be returned.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubLicense

Returns metadata about popular open source licenses




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubLicense -Name mit

Gets the content of the mit license file




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Get-GitHubLicense -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets the content of the license file for the Microsoft\PowerShellForGitHub repository.
It may be necessary to convert the content of the file.  Check the 'encoding' property of
the result to know how 'content' is encoded.  As an example, to convert from Base64, do
the following:

[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($result.content))

---
## Get-GitHubMilestone

### Synopsis



### Syntax

Get-GitHubMilestone -OwnerName <String> -RepositoryName <String> [-State <String>] [-Sort <String>] [-Direction <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

Get-GitHubMilestone -OwnerName <String> -RepositoryName <String> -Milestone <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubMilestone -Uri <String> [-State <String>] [-Sort <String>] [-Direction <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubMilestone -Uri <String> -Milestone <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Get the milestones for a given Github repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Milestone <Int64>
	    The number of a specific milestone to get. If not supplied, will return back all milestones for this repository.

	-State <String>
	    Only milestones with this state are returned.

	-Sort <String>
	    How to sort the results.

	-Direction <String>
	    How to list the results. Ignored without the sort parameter.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubMilestone -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the milestones for the Microsoft\PowerShellForGitHub project.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubMilestone -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -Milestone 1

Get milestone number 1 for the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubOrganizationMember

### Synopsis

Retrieve list of members within an organization.

### Syntax

Get-GitHubOrganizationMember [-OrganizationName] <String> [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve list of members within an organization.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OrganizationName <String>
	    The name of the organization

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubOrganizationMember -OrganizationName PowerShell

---
## Get-GitHubPathTraffic

### Synopsis

Get the top 10 popular contents over the last 14 days for a given Github repository.

### Syntax

Get-GitHubPathTraffic [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubPathTraffic -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Get the top 10 popular contents over the last 14 days for a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubPathTraffic -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the top 10 popular contents over the last 14 days from the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubPullRequest

### Synopsis

Retrieve the pull requests in the specified repository.

### Syntax

Get-GitHubPullRequest [-OwnerName <String>] [-RepositoryName <String>] [-PullRequest <String>] [-State <String>] [-Head <String>] [-Base <String>] [-Sort <String>] [-Direction <String>] 
[-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubPullRequest -Uri <String> [-PullRequest <String>] [-State <String>] [-Head <String>] [-Base <String>] [-Sort <String>] [-Direction <String>] [-AccessToken <String>] [-NoStatus] 
[-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve the pull requests in the specified repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-PullRequest <String>
	    The specic pull request id to return back.  If not supplied, will return back all
	    pull requests for the specified Repository.

	-State <String>
	    The state of the pull requests that should be returned back.

	-Head <String>
	    Filter pulls by head user and branch name in the format of 'user:ref-name'

	-Base <String>
	    Base branch name to filter the pulls by.

	-Sort <String>
	    What to sort the results by.
	    * created
	    * updated
	    * popularity (comment count)
	    * long-running (age, filtering by pulls updated in the last month)

	-Direction <String>
	    The direction to be used for Sort.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>$pullRequests = Get-GitHubPullRequest -Uri 'https://github.com/PowerShell/PowerShellForGitHub'






-------------------------- EXAMPLE 2 --------------------------

PS C:\>$pullRequests = Get-GitHubPullRequest -OwnerName Microsoft -RepositoryName PowerShellForGitHub -State Closed

---
## Get-GitHubRateLimit

### Synopsis

Gets the current rate limit status for the GitHub API based on the currently configured
authentication (Access Token).

### Syntax

Get-GitHubRateLimit [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets the current rate limit status for the GitHub API based on the currently configured
authentication (Access Token).

Use Set-GitHubAuthentication to change your current authentication (Access Token).

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRateLimit

---
## Get-GitHubReferrerTraffic

### Synopsis

Get the top 10 referrers over the last 14 days for a given GitHub repository.

### Syntax

Get-GitHubReferrerTraffic [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubReferrerTraffic -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Get the top 10 referrers over the last 14 days for a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubReferrerTraffic -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the top 10 referrers over the last 14 days from the Microsoft\PowerShellForGitHub project.

---
## Get-GitHubRepository

### Synopsis

Retrieves information about a repository or list of repoistories on GitHub.

### Syntax

Get-GitHubRepository [-OwnerName <String>] [-RepositoryName <String>] [-Visibility <String>] [-Affiliation <String[]>] [-Type <String>] [-Sort <String>] [-Direction <String>] 
[-GetAllPublicRepositories] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepository -Uri <String> [-Visibility <String>] [-Affiliation <String[]>] [-Type <String>] [-Sort <String>] [-Direction <String>] [-GetAllPublicRepositories] [-AccessToken 
<String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepository [-OrganizationName <String>] [-Visibility <String>] [-Affiliation <String[]>] [-Type <String>] [-Sort <String>] [-Direction <String>] [-GetAllPublicRepositories] 
[-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves information about a repository or list of repoistories on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-OrganizationName <String>
	    The name of the organization to retrieve the repositories for.

	-Visibility <String>
	    The type of visibility/accessibility for the repositories to return.

	-Affiliation <String[]>
	    Can be one or more of:
	    
	    owner - Repositories that are owned by the authenticated user
	    
	    collaborator - Repositories that the user has been added to as a collaborator
	    
	    organization_member - Repositories that the user has access to through being
	    a member of an organization.  This includes every repository on every team that the user
	    is on.

	-Type <String>
	    The type of repository to return.

	-Sort <String>
	    Property that the results should be sorted by

	-Direction <String>
	    Direction of the sort that is to be applied to the results.

	-GetAllPublicRepositories <SwitchParameter>
	    If this is specified with no other parameter, then instead of returning back all
	    repositories for the current authenticated user, it will instead return back all
	    public repositories on GitHub.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepository

Gets all repositories for the current authenticated user.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepository -GetAllPublicRepositories

Gets all public repositories on GitHub.




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Get-GitHubRepository -OctoCat OctoCat






-------------------------- EXAMPLE 4 --------------------------

PS C:\>Get-GitHubRepository -Uri https://github.com/PowerShell/PowerShellForGitHub






-------------------------- EXAMPLE 5 --------------------------

PS C:\>Get-GitHubRepository -OrganizationName PowerShell

---
## Get-GitHubRepositoryBranch

### Synopsis

Retrieve branches for a given GitHub repository.

### Syntax

Get-GitHubRepositoryBranch [-OwnerName <String>] [-RepositoryName <String>] [-Name <String>] [-ProtectedOnly] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryBranch -Uri <String> [-Name <String>] [-ProtectedOnly] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve branches for a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Name of the specific branch to be retieved.  If not supplied, all branches will be retrieved.

	-ProtectedOnly <SwitchParameter>

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryBranch -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets all branches for the specified repository.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryBranch -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -Name master

Gets information only on the master branch for the specified repository.

---
## Get-GitHubRepositoryCollaborator

### Synopsis

Retrieve list of contributors for a given repository.

### Syntax

Get-GitHubRepositoryCollaborator [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryCollaborator -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve list of contributors for a given repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryCollaborator -OwnerName Microsoft -RepositoryName PowerShellForGitHub






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryCollaborator -Uri 'https://github.com/PowerShell/PowerShellForGitHub'

---
## Get-GitHubRepositoryContributor

### Synopsis

Retrieve list of contributors for a given repository.

### Syntax

Get-GitHubRepositoryContributor [-OwnerName <String>] [-RepositoryName <String>] [-IncludeAnonymousContributors] [-IncludeStatistics] [-AccessToken <String>] [-NoStatus] [-WhatIf] 
[-Confirm] [<CommonParameters>]

Get-GitHubRepositoryContributor -Uri <String> [-IncludeAnonymousContributors] [-IncludeStatistics] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve list of contributors for a given repository.

GitHub identifies contributors by author email address.
This groups contribution counts by GitHub user, which includes all associated email addresses.
To improve performance, only the first 500 author email addresses in the repository link to
GitHub users. The rest will appear as anonymous contributors without associated GitHub user
information.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-IncludeAnonymousContributors <SwitchParameter>
	    If specified, anonymous contributors will be included in the results.

	-IncludeStatistics <SwitchParameter>
	    If specified, each result will include statistics for the number of additions, deletions
	    and commit counts, by week (excluding merge commits and empty commits).

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryContributor -OwnerName Microsoft -RepositoryName PowerShellForGitHub






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryContributor -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -IncludeStatistics

---
## Get-GitHubRepositoryFork

### Synopsis

Gets the list of forks of the specified repository on GitHub.

### Syntax

Get-GitHubRepositoryFork [-OwnerName <String>] [-RepositoryName <String>] [-Sort <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryFork -Uri <String> [-Sort <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Gets the list of forks of the specified repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Sort <String>
	    The sort order for results.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryFork -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Gets all of the forks for the Microsoft\PowerShellForGitHub repository.

---
## Get-GitHubRepositoryLanguage

### Synopsis

Retrieves a list of the programming languages used in a repository on GitHub.

### Syntax

Get-GitHubRepositoryLanguage [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryLanguage -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves a list of the programming languages used in a repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryLanguage -OwnerName Microsoft -RepositoryName PowerShellForGitHub






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryLanguage -Uri https://github.com/PowerShell/PowerShellForGitHub

---
## Get-GitHubRepositoryTag

### Synopsis

Retrieves tags for a repository on GitHub.

### Syntax

Get-GitHubRepositoryTag [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryTag -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves tags for a repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryTag -OwnerName Microsoft -RepositoryName PowerShellForGitHub






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryTag -Uri https://github.com/PowerShell/PowerShellForGitHub

---
## Get-GitHubRepositoryTopic

### Synopsis

Retrieves information about a repository on GitHub.

### Syntax

Get-GitHubRepositoryTopic [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubRepositoryTopic -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves information about a repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubRepositoryTopic -OwnerName Microsoft -RepositoryName PowerShellForGitHub






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubRepositoryTopic -Uri https://github.com/PowerShell/PowerShellForGitHub

---
## Get-GitHubTeam

### Synopsis

Retrieve a team or teams within an organization or repository on GitHub.

### Syntax

Get-GitHubTeam [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubTeam -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubTeam -OrganizationName <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubTeam -TeamId <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve a team or teams within an organization or repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-OrganizationName <String>
	    The name of the organization

	-TeamId <String>
	    The ID of the speific team to retrieve

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubTeam -OrganizationName PowerShell

---
## Get-GitHubTeamMember

### Synopsis

Retrieve list of team members within an organization.

### Syntax

Get-GitHubTeamMember -OrganizationName <String> -TeamId <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubTeamMember -OrganizationName <String> -TeamName <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieve list of team members within an organization.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OrganizationName <String>
	    The name of the organization

	-TeamName <String>
	    The name of the team in the organization

	-TeamId <Int64>
	    The ID of the team in the organization

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>$members = Get-GitHubTeamMember -Organization PowerShell -TeamName Everybody

---
## Get-GitHubUser

### Synopsis

Retrieves information about the specified user on GitHub.

### Syntax

Get-GitHubUser [-User <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubUser [-Current] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves information about the specified user on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-User <String>
	    The GitHub user to retrieve information for.
	    If not specified, will retrieve information on all GitHub users (and may take a while to complete).

	-Current <SwitchParameter>
	    If specified, gets information on the current user.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubUser -User octocat

Gets information on just the user named 'octocat'




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubUser

Gets information on every GitHub user.




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Get-GitHubUser -Current

Gets information on the current authenticated user.

---
## Get-GitHubUserContextualInformation

### Synopsis

Retrieves contextual information about the specified user on GitHub.

### Syntax

Get-GitHubUserContextualInformation [-User] <String> [[-Subject] <String>] [[-SubjectId] <String>] [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Retrieves contextual information about the specified user on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-User <String>
	    The GitHub user to retrieve information for.

	-Subject <String>
	    Identifies which additional information to receive about the user's hovercard.

	-SubjectId <String>
	    The ID for the Subject.  Required when Subject has been specified.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubUserContextualInformation -User octocat






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Get-GitHubUserContextualInformation -User octocat -Subject Repository -SubjectId 1300192

---
## Get-GitHubViewTraffic

### Synopsis

Get the total number of views and breakdown per day or week for the last 14 days for the given Github Repository.

### Syntax

Get-GitHubViewTraffic [-OwnerName <String>] [-RepositoryName <String>] [-Per <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Get-GitHubViewTraffic -Uri <String> [-Per <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Get the total number of views and breakdown per day or week for the last 14 days.
Timestamps are aligned to UTC midnight of the beginning of the day or week. Week begins on Monday.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Per <String>
	    The interval at which return to return the view counts.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-GitHubViewTraffic -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Get the total number of views and breakdown per day or week for the last 14 days from the Microsoft\PowerShellForGitHub project.

---
## Group-GitHubIssue

### Synopsis

Groups the provided issues based on the specified grouping criteria.

### Syntax

Group-GitHubIssue -Issue <PSObject[]> -Weeks <Int32> [-DateType <String>] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Groups the provided issues based on the specified grouping criteria.

Currently able to group Issues by week.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Issue <PSObject[]>
	    The Issue(s) to be grouped.

	-Weeks <Int32>
	    The number of weeks to group the Issues by.

	-DateType <String>
	    The date property that should be inspected when determining which week grouping the issue
	    if part of.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>$issues = @()

$issues += Get-GitHubIssue -Uri 'https://github.com/powershell/xpsdesiredstateconfiguration'
$issues += Get-GitHubIssue -Uri 'https://github.com/powershell/xactivedirectory'
$issues | Group-GitHubIssue -Weeks 12 -DateType Closed

---
## Invoke-GHRestMethod

### Synopsis

A wrapper around Invoke-WebRequest that understands the Store API.

### Syntax

Invoke-GHRestMethod [-UriFragment] <String> [-Method] <String> [[-Description] <String>] [[-Body] <String>] [[-AcceptHeader] <String>] [-ExtendedResult] [[-AccessToken] <String>] 
[[-TelemetryEventName] <String>] [[-TelemetryProperties] <Hashtable>] [[-TelemetryExceptionBucket] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

A very heavy wrapper around Invoke-WebRequest that understands the Store API and
how to perform its operation with and without console status updates.  It also
understands how to parse and handle errors from the REST calls.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-UriFragment <String>
	    The unique, tail-end, of the REST URI that indicates what Store REST action will
	    be peformed.  This should not start with a leading "/".

	-Method <String>
	    The type of REST method being peformed.  This only supports a reduced set of the
	    possible REST methods (delete, get, post, put).

	-Description <String>
	    A friendly description of the operation being performed for logging and console
	    display purposes.

	-Body <String>
	    This optional parameter forms the body of a PUT or POST request. It will be automatically
	    encoded to UTF8 and sent as Content Type: "application/json; charset=UTF-8"

	-AcceptHeader <String>
	    Specify the media type in the Accept header.  Different types of commands may require
	    different media types.

	-ExtendedResult <SwitchParameter>
	    If specified, the result will be a PSObject that contains the normal result, along with
	    the response code and other relevant header detail content.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api as opposed to requesting a new one.

	-TelemetryEventName <String>
	    If provided, the successful execution of this REST command will be logged to telemetry
	    using this event name.

	-TelemetryProperties <Hashtable>
	    If provided, the successful execution of this REST command will be logged to telemetry
	    with these additional properties.  This will be silently ignored if TelemetryEventName
	    is not provided as well.

	-TelemetryExceptionBucket <String>
	    If provided, any exception that occurs will be logged to telemetry using this bucket.
	    It's possible that users will wish to log exceptions but not success (by providing
	    TelemetryEventName) if this is being executed as part of a larger scenario.  If this
	    isn't provided, but TelemetryEventName *is* provided, then TelemetryEventName will be
	    used as the exception bucket value in the event of an exception.  If neither is specified,
	    no bucket value will be used.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Invoke-GHRestMethod -UriFragment "applications/" -Method Get -Description "Get first 10 applications"

Gets the first 10 applications for the connected dev account.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Invoke-GHRestMethod -UriFragment "applications/0ABCDEF12345/submissions/1234567890123456789/" -Method Delete -Description "Delete Submission" -NoStatus

Deletes the specified submission, but the request happens in the foreground and there is
no additional status shown to the user until a response is returned from the REST request.

---
## Invoke-GHRestMethodMultipleResult

### Synopsis

A special-case wrapper around Invoke-GHRestMethod that understands GET URI's
which support the 'top' and 'max' parameters.

### Syntax

Invoke-GHRestMethodMultipleResult [-UriFragment] <String> [-Description] <String> [[-AcceptHeader] <String>] [[-AccessToken] <String>] [[-TelemetryEventName] <String>] 
[[-TelemetryProperties] <Hashtable>] [[-TelemetryExceptionBucket] <String>] [-SinglePage] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

A special-case wrapper around Invoke-GHRestMethod that understands GET URI's
which support the 'top' and 'max' parameters.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-UriFragment <String>
	    The unique, tail-end, of the REST URI that indicates what Store REST action will
	    be peformed.  This should *not* include the 'top' and 'max' parameters.  These
	    will be automatically added as needed.

	-Description <String>
	    A friendly description of the operation being performed for logging and console
	    display purposes.

	-AcceptHeader <String>
	    Specify the media type in the Accept header.  Different types of commands may require
	    different media types.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api as opposed to requesting a new one.

	-TelemetryEventName <String>
	    If provided, the successful execution of this REST command will be logged to telemetry
	    using this event name.

	-TelemetryProperties <Hashtable>
	    If provided, the successful execution of this REST command will be logged to telemetry
	    with these additional properties.  This will be silently ignored if TelemetryEventName
	    is not provided as well.

	-TelemetryExceptionBucket <String>
	    If provided, any exception that occurs will be logged to telemetry using this bucket.
	    It's possible that users will wish to log exceptions but not success (by providing
	    TelemetryEventName) if this is being executed as part of a larger scenario.  If this
	    isn't provided, but TelemetryEventName *is* provided, then TelemetryEventName will be
	    used as the exception bucket value in the event of an exception.  If neither is specified,
	    no bucket value will be used.

	-SinglePage <SwitchParameter>
	    By default, this function will automtically call any follow-up "nextLinks" provided by
	    the return value in order to retrieve the entire result set.  If this switch is provided,
	    only the first "page" of results will be retrieved, and the "nextLink" links will not be
	    followed.
	    WARNING: This might take a while depending on how many results there are.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Invoke-GHRestMethodMultipleResult -UriFragment "repos/PowerShell/PowerShellForGitHub/issues?state=all" -Description "Get all issues"

Gets the first set of issues associated with this project,
with the console window showing progress while awaiting the response
from the REST request.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Invoke-GHRestMethodMultipleResult -UriFragment "repos/PowerShell/PowerShellForGitHub/issues?state=all" -Description "Get all issues" -NoStatus

Gets the first set of issues associated with this project,
but the request happens in the foreground and there is no additional status
shown to the user until a response is returned from the REST request.

---
## Lock-GitHubIssue

### Synopsis

Lock an Issue or Pull Request conversation on GitHub.

### Syntax

Lock-GitHubIssue [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> [-Reason <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Lock-GitHubIssue -Uri <String> -Issue <Int64> [-Reason <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Lock an Issue or Pull Request conversation on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    The issue to be locked.

	-Reason <String>
	    The reason for locking the issue or pull request conversation.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Lock-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 4 -Title 'Test Issue' -Reason Spam

---
## Move-GitHubRepositoryOwnership

### Synopsis

Creates a new repository on GitHub.

### Syntax

Move-GitHubRepositoryOwnership [-OwnerName <String>] [-RepositoryName <String>] -NewOwnerName <String> [-TeamId <Int64[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

Move-GitHubRepositoryOwnership -Uri <String> -NewOwnerName <String> [-TeamId <Int64[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-NewOwnerName <String>
	    The username or organization name the repository will be transferred to.

	-TeamId <Int64[]>
	    ID of the team or teams to add to the repository.  Teams can only be added to
	    organization-owned repositories.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Move-GitHubRepositoryOwnership -OwnerName Microsoft -RepositoryName PowerShellForGitHub -NewOwnerName OctoCat

---
## New-GithubAssignee

### Synopsis



### Syntax

New-GithubAssignee [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> -Assignee <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

New-GithubAssignee -Uri <String> -Issue <Int64> -Assignee <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Adds a list of assignees to a Github Issue for the given repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to add the assignees to.

	-Assignee <String[]>
	    Usernames of users to assign this issue to. NOTE: Only users with push access can add assignees to an issue.
	    Assignees are silently ignored otherwise.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GithubAssignee -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Assignee $assignee

Lists the available assignees for issues from the Microsoft\PowerShellForGitHub project.

---
## New-GitHubComment

### Synopsis



### Syntax

New-GitHubComment [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> -Body <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

New-GitHubComment -Uri <String> -Issue <Int64> -Body <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new Github comment in an issue for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    The number for the issue that the comment will be filed under.

	-Body <String>
	    The contents of the comment.

	-MediaType <String>
	    The format in which the API will return the body of the comment.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubComment -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 1 -Body "Testing this API"

Creates a new Github comment in an issue for the Microsoft\PowerShellForGitHub project.

---
## New-GitHubIssue

### Synopsis

Create a new Issue on GitHub.

### Syntax

New-GitHubIssue [-OwnerName <String>] [-RepositoryName <String>] -Title <String> [-Body <String>] [-Assignee <String[]>] [-Milestone <Int64>] [-Label <String[]>] [-MediaType <String>] 
[-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

New-GitHubIssue -Uri <String> -Title <String> [-Body <String>] [-Assignee <String[]>] [-Milestone <Int64>] [-Label <String[]>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] 
[-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Create a new Issue on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Title <String>
	    The title of the issue

	-Body <String>
	    The contents of the issue

	-Assignee <String[]>
	    Login(s) for Users to assign to the issue.

	-Milestone <Int64>
	    The number of the mileston to associate this issue with.

	-Label <String[]>
	    Label(s) to associate with this issue.

	-MediaType <String>
	    The format in which the API will return the body of the issue.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Title 'Test Issue'

---
## New-GitHubLabel

### Synopsis

Create a new label on a given GitHub repository.

### Syntax

New-GitHubLabel [-OwnerName <String>] [-RepositoryName <String>] -Name <String> -Color <String> [-Description <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

New-GitHubLabel -Uri <String> -Name <String> -Color <String> [-Description <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Create a new label on a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Name of the label to be created.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-Color <String>
	    Color (in HEX) for the new label, without the leading # sign.

	-Description <String>
	    A short description of the label.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Name TestLabel -Color BBBBBB

Creates a new, grey-colored label called "TestLabel" in the PowerShellForGitHub project.

---
## New-GitHubMilestone

### Synopsis



### Syntax

New-GitHubMilestone -OwnerName <String> -RepositoryName <String> -Title <String> [-State <String>] [-Description <String>] [-DueOn <DateTime>] [-AccessToken <String>] [-NoStatus] [-WhatIf] 
[-Confirm] [<CommonParameters>]

New-GitHubMilestone -Uri <String> -Title <String> [-State <String>] [-Description <String>] [-DueOn <DateTime>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new Github milestone for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Title <String>
	    The title of the milestone.

	-State <String>
	    The state of the milestone.

	-Description <String>
	    A description of the milestone.

	-DueOn <DateTime>
	    The milestone due date.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubMilestone -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Title "Testing this API"

Creates a new Github milestone for the Microsoft\PowerShellForGitHub project.

---
## New-GitHubRepository

### Synopsis

Creates a new repository on GitHub.

### Syntax

New-GitHubRepository [-RepositoryName] <String> [[-OrganizationName] <String>] [[-Description] <String>] [[-Homepage] <String>] [[-GitIgnoreTemplate] <String>] [[-LicenseTemplate] 
<String>] [[-TeamId] <Int64>] [-Private] [-NoIssues] [-NoProjects] [-NoWiki] [-AutoInit] [-DisallowSquashMerge] [-DisallowMergeCommit] [-DisallowRebaseMerge] [[-AccessToken] <String>] 
[-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-RepositoryName <String>
	    Name of the repository to be created.

	-OrganizationName <String>
	    Name of the organization that the repository should be created under.
	    If not specified, will be created under the current user's account.

	-Description <String>
	    A short description of the repository.

	-Homepage <String>
	    A URL with more information about the repository.

	-GitIgnoreTemplate <String>
	    Desired language or platform .gitignore template to apply.
	    For supported values, call Get-GitHubGitIgnore.
	    Values are case-sensitive.

	-LicenseTemplate <String>
	    Choose an open source license template that best suits your needs.
	    For supported values, call Get-GitHubLicense
	    Values are case-sensitive.

	-TeamId <Int64>
	    The id of the team that will be granted access to this repository.
	    This is only valid when creating a repository in an organization.

	-Private <SwitchParameter>
	    By default, this repository will created Public.  Specify this to create
	    a private repository.  Creating private repositories requires a paid GitHub account.

	-NoIssues <SwitchParameter>
	    By default, this repository will support Issues.  Specify this to disable Issues.

	-NoProjects <SwitchParameter>
	    By default, this repository will support Projects.  Specify this to disable Projects.
	    If you're creating a repository in an organization that has disabled repository projects,
	    this will be true by default.

	-NoWiki <SwitchParameter>
	    By default, this repository will have a Wiki.  Specify this to disable the Wiki.

	-AutoInit <SwitchParameter>
	    Specify this to create an initial commit with an empty README.

	-DisallowSquashMerge <SwitchParameter>
	    By default, squash-merging pull requests will be allowed.
	    Specify this to disallow.

	-DisallowMergeCommit <SwitchParameter>
	    By default, merging pull requests with a merge commit will be allowed.
	    Specify this to disallow.

	-DisallowRebaseMerge <SwitchParameter>
	    By default, rebase-merge pull requests will be allowed.
	    Specify this to disallow.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubRepository -RepositoryName MyNewRepo -AutoInit






-------------------------- EXAMPLE 2 --------------------------

PS C:\>New-GitHubRepository -RepositoryName MyNewRepo -Organization MyOrg -DisallowRebaseMerge

---
## New-GitHubRepositoryFork

### Synopsis

Creates a new fork of a repository on GitHub.

### Syntax

New-GitHubRepositoryFork [-OwnerName <String>] [-RepositoryName <String>] [-OrganizationName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

New-GitHubRepositoryFork -Uri <String> [-OrganizationName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Creates a new fork of a repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-OrganizationName <String>
	    Name of the organization that the new repository should be created under.
	    If not specified, will be created under the current authenticated user's account.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>New-GitHubRepositoryFork -OwnerName Microsoft -RepositoryName PowerShellForGitHub

Creates a fork of this repository under the current authenticated user's account.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>New-GitHubRepositoryFork -OwnerName Microsoft -RepositoryName PowerShellForGitHub -OrganizationName OctoLabs

Creates a fork of this repository under the OctoLabs organization.

---
## Remove-GithubAssignee

### Synopsis



### Syntax

Remove-GithubAssignee [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> -Assignee <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GithubAssignee -Uri <String> -Issue <Int64> -Assignee <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Removes an assignee from a Github issue.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to remove the assignees from.

	-Assignee <String[]>
	    Usernames of assignees to remove from an issue. NOTE: Only users with push access can remove assignees from an issue. Assignees are silently ignored otherwise.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GithubAssignee -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Assignee $assignees

Lists the available assignees for issues from the Microsoft\PowerShellForGitHub project.

---
## Remove-GitHubComment

### Synopsis



### Syntax

Remove-GitHubComment [-OwnerName <String>] [-RepositoryName <String>] -CommentID <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubComment -Uri <String> -CommentID <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a Github comment for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-CommentID <String>
	    The id of the comment to delete.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubComment -OwnerName Microsoft -RepositoryName PowerShellForGitHub -CommentID 1

Deletes a Github comment from the Microsoft\PowerShellForGitHub project.

---
## Remove-GitHubIssueLabel

### Synopsis



### Syntax

Remove-GitHubIssueLabel -OwnerName <String> -RepositoryName <String> -Issue <Int64> [-Name <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubIssueLabel -Uri <String> -Issue <Int64> [-Name <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a label from an issue in the given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to remove the label from.

	-Name <String>
	    Name of the label to be deleted. If not provided, will delete all labels on the issue.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubIssueLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Name TestLabel -Issue 1

Removes the label called "TestLabel" from issue 1 in the PowerShellForGitHub project.

---
## Remove-GitHubLabel

### Synopsis

Deletes a label from a given GitHub repository.

### Syntax

Remove-GitHubLabel [-OwnerName <String>] [-RepositoryName <String>] -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubLabel -Uri <String> -Name <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a label from a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Name of the label to be deleted.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Name TestLabel

Removes the label called "TestLabel" from the PowerShellForGitHub project.

---
## Remove-GitHubMilestone

### Synopsis



### Syntax

Remove-GitHubMilestone -OwnerName <String> -RepositoryName <String> -Milestone <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubMilestone -Uri <String> -Milestone <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Deletes a Github milestone for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Milestone <String>
	    The number of a specific milestone to delete.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubMilestone -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Milestone 1

Deletes a Github milestone from the Microsoft\PowerShellForGitHub project.

---
## Remove-GitHubRepository

### Synopsis

Removes/deletes a repository from GitHub.

### Syntax

Remove-GitHubRepository [-OwnerName <String>] [-RepositoryName <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-GitHubRepository -Uri <String> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Removes/deletes a repository from GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Remove-GitHubRepository -OwnerName You -RepositoryName YourRepoToDelete






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Remove-GitHubRepository -Uri https://github.com/You/YourRepoToDelete

---
## Reset-GitHubConfiguration

### Synopsis

Clears out the user's configuration file and configures this session with all default
configuration values.

### Syntax

Reset-GitHubConfiguration [-SessionOnly] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Clears out the user's configuration file and configures this session with all default
configuration values.

This would be the functional equivalent of using this on a completely different computer.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-SessionOnly <SwitchParameter>
	    By default, this will delete the location configuration file so that all defaults are used
	    again.  If this is specified, then only the configuration values that were made during
	    this session will be discarded.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Reset-GitHubConfiguration

Deletes the local configuration file and loads in all default configration values.

---
## Restore-GitHubConfiguration

### Synopsis

Sets the specified file to be the user's configuration file.

### Syntax

Restore-GitHubConfiguration [[-Path] <String>] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Sets the specified file to be the user's configuration file.

This is primarily used for unit testing scenarios.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Path <String>
	    The path to store the user's current configuration file.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Restore-GitHubConfiguration -Path 'c:\foo\config.json'

Makes the contents of c:\foo\config.json be the user's configuration for the module.

---
## Set-GitHubAuthentication

### Synopsis

Allows the user to configure the API token that should be used for authentication
with the GitHub API.

### Syntax

Set-GitHubAuthentication [[-Credential] <PSCredential>] [-SessionOnly] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Allows the user to configure the API token that should be used for authentication
with the GitHub API.

The token will be stored on the machine as a SecureString and will automatically
be read on future PowerShell sessions with this module.  If the user ever wishes
to remove their authentication from the system, they simply need to call
Clear-GitHubAuthentication.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Credential <PSCredential>
	    If provided, instead of prompting the user for their API Token, it will be extracted
	    from the password field of this credential object.

	-SessionOnly <SwitchParameter>
	    By default, this method will store the provided API Token as a SecureString in a local
	    file so that it can be restored automatically in future PowerShell sessions.  If this
	    switch is provided, the file will not be created/updated and the authentication information
	    will only remain in memory for the duration of this PowerShell session.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubAuthentication

Prompts the user for their GitHub API Token and stores it in a file on the machine as a
SecureString for use in future PowerShell sessions.




-------------------------- EXAMPLE 2 --------------------------

$secureString = ("<Your Access Token>" | ConvertTo-SecureString)

$cred = New-Object System.Management.Automation.PSCredential "username is ignored", $secureString
Set-GitHubAuthentication -Credential $cred

Uses the API token stored in the password field of the provided credential object for
authentication, and stores it in a file on the machine as a SecureString for use in
future PowerShell sessions.




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Set-GitHubAuthentication -SessionOnly

Prompts the user for their GitHub API Token, but keeps it in memory only for the duration
of this PowerShell session.




-------------------------- EXAMPLE 4 --------------------------

PS C:\>Set-GitHubAuthentication -Credential $cred -SessionOnly

Uses the API token stored in the password field of the provided credential object for
authentication, but keeps it in memory only for the duration of this PowerShell session..

---
## Set-GitHubComment

### Synopsis



### Syntax

Set-GitHubComment [-OwnerName <String>] [-RepositoryName <String>] -CommentID <String> -Body <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

Set-GitHubComment -Uri <String> -CommentID <String> -Body <String> [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Set an existing comment in an issue for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-CommentID <String>
	    The comment ID of the comment to edit.

	-Body <String>
	    The new contents of the comment.

	-MediaType <String>
	    The format in which the API will return the body of the comment.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubComment -OwnerName Microsoft -RepositoryName PowerShellForGitHub -CommentID 1 -Body "Testing this API"

Update an existing comment in an issue for the Microsoft\PowerShellForGitHub project.

---
## Set-GitHubConfiguration

### Synopsis

Change the value of a configuration property for the PowerShellForGitHub module,
for the sesion only, or globally for this user.

### Syntax

Set-GitHubConfiguration [[-ApiHostName] <String>] [[-ApplicationInsightsKey] <String>] [[-AssemblyPath] <String>] [-DefaultNoStatus] [[-DefaultOwnerName] <String>] 
[[-DefaultRepositoryName] <String>] [-DisableLogging] [-DisablePiiProtection] [-DisableSmarterObjects] [-DisableTelemetry] [[-LogPath] <String>] [-LogProcessId] [-LogRequestBody] 
[-LogTimeAsUtc] [[-RetryDelaySeconds] <Int32>] [-SuppressNoTokenWarning] [-SuppressTelemetryReminder] [[-WebRequestTimeoutSec] <Int32>] [-SessionOnly] [-WhatIf] [-Confirm] 
[<CommonParameters>]

### Description

Change the value of a configuration property for the PowerShellForGitHub module,
for the sesion only, or globally for this user.

A single call to this method can set any number or combination of properties.

To change any of the boolean/switch properties to false, specify the switch,
immediately followed by ":$false" with no space.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-ApiHostName <String>
	    The hostname of the GitHub instance to communicate with. Defaults to 'github.com'. Provide a
	    different hostname when using a GitHub Enterprise server. Do not include the HTTP/S prefix,
	    and do not include 'api'. For example, use "github.contoso.com".

	-ApplicationInsightsKey <String>
	    Change the Application Insights instance that telemetry will be reported to (if telemetry
	    hasn't been disabled via DisableTelemetry).

	-AssemblyPath <String>
	    The location that any dependent assemblies that this module depends on can be located.
	    If the assemblies can't be found at this location, nor in a temporary cache or in
	    the module's directory, the assemblies will be downloaded and temporarily cached.

	-DefaultNoStatus <SwitchParameter>
	    Control if the -NoStatus switch should be passed-in by default to all methods.

	-DefaultOwnerName <String>
	    The owner name that should be used with a command that takes OwnerName as a parameter
	    when no value has been supplied.

	-DefaultRepositoryName <String>
	    The owner name that should be used with a command that takes RepositoryName as a parameter
	    when no value has been supplied.

	-DisableLogging <SwitchParameter>
	    Specify this switch to stop the module from logging all activity to a log file located
	    at the location specified by LogPath.

	-DisablePiiProtection <SwitchParameter>
	    Specify this switch to disable the hashing of potential PII data prior to submitting the
	    data to telemetry (if telemetry hasn't been disabled via DisableTelemetry).

	-DisableSmarterObjects <SwitchParameter>
	    By deffault, this module will modify all objects returned by the API calls to update
	    any properties that can be converted to objects (like strings for Date/Time's being
	    converted to real DateTime objects).  Enable this property if you desire getting back
	    the unmodified version of the object from the API.

	-DisableTelemetry <SwitchParameter>
	    Specify this switch to stop the module from reporting any of its usage (which would be used
	    for diagnostics purposes).

	-LogPath <String>
	    The location of the log file that all activity will be written to if DisableLogging remains
	    $false.

	-LogProcessId <SwitchParameter>
	    If specified, the Process ID of the current PowerShell session will be included in each
	    log entry.  This can be useful if you have concurrent PowerShell sessions all logging
	    to the same file, as it would then be possible to filter results based on ProcessId.

	-LogRequestBody <SwitchParameter>
	    If specified, the JSON body of the REST request will be logged to verbose output.
	    This can be helpful for debugging purposes.

	-LogTimeAsUtc <SwitchParameter>
	    If specified, all times logged will be logged as UTC instead of the local timezone.

	-RetryDelaySeconds <Int32>
	    The number of seconds to wait before retrying a command again after receiving a 202 response.

	-SuppressNoTokenWarning <SwitchParameter>
	    If an Access Token has not been configured, this module will provide a warning to the user
	    informing them of this, once per session.  If it is expected that this module will regularly
	    be used without configuring an Access Token, specify this switch to always suppress that
	    warning message.

	-SuppressTelemetryReminder <SwitchParameter>
	    When telemetry is enabled, a warning will be printed to the console once per session
	    informing users that telemetry is occurring.  Setting this value will suppress that
	    message from showing up ever again.

	-WebRequestTimeoutSec <Int32>
	    The number of seconds that should be allowed before an API request times out.  A value of
	    0 indicates an infinite timeout, however experience has shown that PowerShell doesn't seem
	    to always honor inifinite timeouts.  Hence, this value can be configured if need be.

	-SessionOnly <SwitchParameter>
	    By default, this method will store the configuration values in a local file so that changes
	    persist across PowerShell sessions.  If this switch is provided, the file will not be
	    created/updated and the specified configuration changes will only remain in memory/effect
	    for the duration of this PowerShell session.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubConfiguration -WebRequestTimeoutSec 120 -SuppressNoTokenWarning

Changes the timeout permitted for a web request to two minutes, and additionally tells
the module to never warn about no Access Token being configured.  These settings will be
persisted across future PowerShell sessions.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Set-GitHubConfiguration -DisableLogging -SessionOnly

Disables the logging of any activity to the logfile specified in LogPath, but for this
session only.




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Set-GitHubConfiguration -ApiHostName "github.contoso.com"

Sets all requests to connect to a GitHub Enterprise server running at
github.contoso.com.

---
## Set-GitHubIssueLabel

### Synopsis



### Syntax

Set-GitHubIssueLabel [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubIssueLabel -Uri <String> -Issue <Int64> -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Replaces labels on an issue in the given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    Issue number to replace the labels.

	-Name <String[]>

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubIssueLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 1 -LabelName $labels

Replaces labels on an issue in the PowerShellForGitHub project.

---
## Set-GitHubLabel

### Synopsis

Sets the entire set of Labels on the given GitHub repository to match the provided list
of Labels.

### Syntax

Set-GitHubLabel [-OwnerName <String>] [-RepositoryName <String>] [-Label <Object[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubLabel -Uri <String> [-Label <Object[]>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Sets the entire set of Labels on the given GitHub repository to match the provided list
of Labels.

Will update the color/description for any Labels already in the repository that match the
name of a Label in the provided list.  All other existing Labels will be removed, and then
new Labels will be created to match the others in the Label list.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Label <Object[]>
	    The array of Labels (name, color, description) that the repository should be aligning to.
	    A default list of labels will be used if no Labels are provided.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Label @(@{'name' = 'TestLabel'; 'color' = 'EEEEEE'}, @{'name' = 'critical'; 'color' = 'FF000000'; 
'description' = 'Needs immediate attention'})

Removes any labels not in this Label array, ensure the current assigned color and descriptions
match what's in the array for the labels that do already exist, and then creates new labels
for any remaining ones in the Label list.

---
## Set-GitHubMilestone

### Synopsis



### Syntax

Set-GitHubMilestone -OwnerName <String> -RepositoryName <String> -Milestone <Int64> -Title <String> [-State <String>] [-Description <String>] [-DueOn <DateTime>] [-AccessToken <String>] 
[-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubMilestone -Uri <String> -Milestone <Int64> -Title <String> [-State <String>] [-Description <String>] [-DueOn <DateTime>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] 
[<CommonParameters>]

### Description

Update an existing milestone for the given repository

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Milestone <Int64>
	    The number of a specific milestone to get.

	-Title <String>
	    The title of the milestone.

	-State <String>
	    The state of the milestone.

	-Description <String>
	    A description of the milestone.

	-DueOn <DateTime>
	    The milestone due date.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubMilestone -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Milestone 1 -Title "Testing this API"

Update an existing milestone for the Microsoft\PowerShellForGitHub project.

---
## Set-GitHubRepositoryTopic

### Synopsis

Replaces all topics for a repository on GitHub.

### Syntax

Set-GitHubRepositoryTopic [-OwnerName <String>] [-RepositoryName <String>] -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubRepositoryTopic [-OwnerName <String>] [-RepositoryName <String>] -Clear [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubRepositoryTopic -Uri <String> -Clear [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Set-GitHubRepositoryTopic -Uri <String> -Name <String[]> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Replaces all topics for a repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String[]>
	    Array of topics to add to the repository.

	-Clear <SwitchParameter>
	    Specify this to clear all topics from the repository.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Set-GitHubRepositoryTopic -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Clear






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Set-GitHubRepositoryTopic -Uri https://github.com/PowerShell/PowerShellForGitHub -Name ('octocat', 'powershell', 'github')

---
## Split-GitHubUri

### Synopsis

Extracts the relevant elements of a GitHub repository Uri and returns the requested element.

### Syntax

Split-GitHubUri -Uri <String> [-RepositoryName] [<CommonParameters>]

Split-GitHubUri -Uri <String> [-OwnerName] [<CommonParameters>]

### Description

Extracts the relevant elements of a GitHub repository Uri and returns the requested element.

Currently supports retrieving the OwnerName and the RepositoryName, when avaialable.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Uri <String>
	    The GitHub repository Uri whose components should be returned.

	-OwnerName <SwitchParameter>
	    Returns the Owner Name from the Uri if it can be identified.

	-RepositoryName <SwitchParameter>
	    Returns the Repository Name from the Uri if it can be identified.

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Split-GitHubUri -Uri 'https://github.com/PowerShell/PowerShellForGitHub'

PowerShellForGitHub




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Split-GitHubUri -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -RepositoryName

PowerShellForGitHub




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Split-GitHubUri -Uri 'https://github.com/PowerShell/PowerShellForGitHub' -OwnerName

PowerShell

---
## Test-GitHubAssignee

### Synopsis



### Syntax

Test-GitHubAssignee [-OwnerName <String>] [-RepositoryName <String>] [-Assignee <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Test-GitHubAssignee -Uri <String> [-Assignee <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Checks if a user has permission to be assigned to an issue in this repository. Returns a boolean.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Assignee <String>
	    Username for the assignee

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Test-GitHubAssignee -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Assignee "LoginID123"

Checks if a user has permission to be assigned to an issue from the Microsoft\PowerShellForGitHub project.

---
## Test-GitHubAuthenticationConfigured

### Synopsis

Indicates if a GitHub API Token has been configured for this module via Set-GitHubAuthentication.

### Syntax

Test-GitHubAuthenticationConfigured [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Indicates if a GitHub API Token has been configured for this module via Set-GitHubAuthentication.

The Git repo for this module can be found here: http://aka.ms/PowershellForGitHub

### Parameters

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Test-GitHubAuthenticationConfigured

Returns $true if the session is authenticated; $false otherwise

---
## Test-GitHubOrganizationMember

### Synopsis

Check to see if a user is a member of an organization.

### Syntax

Test-GitHubOrganizationMember [-OrganizationName] <String> [-UserName] <String> [[-AccessToken] <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Check to see if a user is a member of an organization.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OrganizationName <String>
	    The name of the organization.

	-UserName <String>
	    The name of the user being inquired about.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Test-GitHubOrganizationMember -OrganizationName PowerShell -UserName Octocat

---
## Unlock-GitHubIssue

### Synopsis

Unlocks an Issue or Pull Request conversation on GitHub.

### Syntax

Unlock-GitHubIssue [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Unlock-GitHubIssue -Uri <String> -Issue <Int64> [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Unlocks an Issue or Pull Request conversation on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    The issue to be unlocked.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Unlock-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 4

---
## Update-GitHubCurrentUser

### Synopsis

Updates information about the current authenticated user on GitHub.

### Syntax

Update-GitHubCurrentUser [[-Name] <String>] [[-Email] <String>] [[-Blog] <String>] [[-Company] <String>] [[-Location] <String>] [[-Bio] <String>] [-Hireable] [[-AccessToken] <String>] 
[-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Updates information about the current authenticated user on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-Name <String>
	    The new name of the user.

	-Email <String>
	    The publicly visible email address of the user.

	-Blog <String>
	    The new blog URL of the user.

	-Company <String>
	    The new company of the user.

	-Location <String>
	    The new location of the user.

	-Bio <String>
	    The new short biography of the user.

	-Hireable <SwitchParameter>
	    Specify to indicate a change in hireable availability for the current authenticated user's
	    GitHub profile.  To change to "not hireable", specify -Hireable:$false

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Update-GitHubCurrentUser -Location 'Seattle, WA' -Hireable:$false

Updates the current user to indicate that their location is "Seattle, WA" and that they
are not currently hireable.

---
## Update-GitHubIssue

### Synopsis

Create a new Issue on GitHub.

### Syntax

Update-GitHubIssue [-OwnerName <String>] [-RepositoryName <String>] -Issue <Int64> [-Title <String>] [-Body <String>] [-Assignee <String[]>] [-Milestone <Int64>] [-Label <String[]>] 
[-State <String>] [-MediaType <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Update-GitHubIssue -Uri <String> -Issue <Int64> [-Title <String>] [-Body <String>] [-Assignee <String[]>] [-Milestone <Int64>] [-Label <String[]>] [-State <String>] [-MediaType <String>] 
[-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Create a new Issue on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Issue <Int64>
	    The issue to be updated.

	-Title <String>
	    The title of the issue

	-Body <String>
	    The contents of the issue

	-Assignee <String[]>
	    Login(s) for Users to assign to the issue.
	    Provide an empty array to clear all existing assignees.

	-Milestone <Int64>
	    The number of the mileston to associate this issue with.
	    Set to 0/$null to remove current.

	-Label <String[]>
	    Label(s) to associate with this issue.
	    Provide an empty array to clear all existing labels.

	-State <String>
	    Modify the current state of the issue.

	-MediaType <String>
	    The format in which the API will return the body of the issue.
	    
	    Raw - Return the raw markdown body. Response will include body. This is the default if you do not pass any specific media type.
	    Text - Return a text only representation of the markdown body. Response will include body_text.
	    Html - Return HTML rendered from the body's markdown. Response will include body_html.
	    Full - Return raw, text and HTML representations. Response will include body, body_text, and body_html.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Update-GitHubIssue -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Issue 4 -Title 'Test Issue' -State Closed

---
## Update-GitHubLabel

### Synopsis

Updates an existing label on a given GitHub repository.

### Syntax

Update-GitHubLabel [-OwnerName <String>] [-RepositoryName <String>] -Name <String> -NewName <String> -Color <String> [-Description <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] 
[-Confirm] [<CommonParameters>]

Update-GitHubLabel -Uri <String> -Name <String> -NewName <String> -Color <String> [-Description <String>] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Updates an existing label on a given GitHub repository.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Name <String>
	    Current name of the label to be updated.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-NewName <String>
	    New name for the label being updated.
	    Emoji and codes are supported.  For more information, see here: https://www.webpagefx.com/tools/emoji-cheat-sheet/

	-Color <String>
	    Color (in HEX) for the new label, without the leading # sign.

	-Description <String>
	    A short description of the label.

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Update-GitHubLabel -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Name TestLabel -NewName NewTestLabel -LabelColor BBBB00

Updates the existing label called TestLabel in the PowerShellForGitHub project to be called
'NewTestLabel' and be colored yellow.

---
## Update-GitHubRepository

### Synopsis

Updates the details of an existing repository on GitHub.

### Syntax

Update-GitHubRepository [-OwnerName <String>] [-RepositoryName <String>] [-Description <String>] [-Homepage <String>] [-DefaultBranch <String>] [-Private] [-NoIssues] [-NoProjects] 
[-NoWiki] [-DisallowSquashMerge] [-DisallowMergeCommit] [-DisallowRebaseMerge] [-Archived] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

Update-GitHubRepository -Uri <String> [-Description <String>] [-Homepage <String>] [-DefaultBranch <String>] [-Private] [-NoIssues] [-NoProjects] [-NoWiki] [-DisallowSquashMerge] 
[-DisallowMergeCommit] [-DisallowRebaseMerge] [-Archived] [-AccessToken <String>] [-NoStatus] [-WhatIf] [-Confirm] [<CommonParameters>]

### Description

Updates the details of an existing repository on GitHub.

The Git repo for this module can be found here: http://aka.ms/PowerShellForGitHub

### Parameters

	-OwnerName <String>
	    Owner of the repository.
	    If not supplied here, the DefaultOwnerName configuration property value will be used.

	-RepositoryName <String>
	    Name of the repository.
	    If not supplied here, the DefaultRepositoryName configuration property value will be used.

	-Uri <String>
	    Uri for the repository.
	    The OwnerName and RepositoryName will be extracted from here instead of needing to provide
	    them individually.

	-Description <String>
	    A short description of the repository.

	-Homepage <String>
	    A URL with more information about the repository.

	-DefaultBranch <String>
	    Update the default branch for this repository.

	-Private <SwitchParameter>
	    Specify this to make the repository repository.  Creating private repositories requires a
	    paid GitHub account.
	    To change a repository to be public, specify -Private:$false

	-NoIssues <SwitchParameter>
	    By default, this repository will support Issues.  Specify this to disable Issues.

	-NoProjects <SwitchParameter>
	    By default, this repository will support Projects.  Specify this to disable Projects.
	    If you're creating a repository in an organization that has disabled repository projects,
	    this will be true by default.

	-NoWiki <SwitchParameter>
	    By default, this repository will have a Wiki.  Specify this to disable the Wiki.

	-DisallowSquashMerge <SwitchParameter>
	    By default, squash-merging pull requests will be allowed.
	    Specify this to disallow.

	-DisallowMergeCommit <SwitchParameter>
	    By default, merging pull requests with a merge commit will be allowed.
	    Specify this to disallow.

	-DisallowRebaseMerge <SwitchParameter>
	    By default, rebase-merge pull requests will be allowed.
	    Specify this to disallow.

	-Archived <SwitchParameter>

	-AccessToken <String>
	    If provided, this will be used as the AccessToken for authentication with the
	    REST Api.  Otherwise, will attempt to use the configured value or will run unauthenticated.

	-NoStatus <SwitchParameter>
	    If this switch is specified, long-running commands will run on the main thread
	    with no commandline status update.  When not specified, those commands run in
	    the background, enabling the command prompt to provide status information.
	    If not supplied here, the DefaultNoStatus configuration property value will be used.

	-WhatIf <SwitchParameter>

	-Confirm <SwitchParameter>

### Examples

-------------------------- EXAMPLE 1 --------------------------

PS C:\>Update-GitHubRepository -OwnerName Microsoft -RepositoryName PowerShellForGitHub -Description 'The best way to automate your GitHub interactions'






-------------------------- EXAMPLE 2 --------------------------

PS C:\>Update-GitHubRepository -Uri https://github.com/PowerShell/PowerShellForGitHub -Private:$false

---

