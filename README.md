JotX - improved and completed Jot
---------------------------------

### Configuration from the file.
All parameters and templates can be specified in one file.

```php
    [!JotX? &config=`faq` !] - Вопрос-Ответ
    [!JotX? &config=`tree` !] - Древовидные комментарии
    [!JotX? &config=`tree-ajax` !] - Древовидные комментарии с аякс
```
### Modes are put into files.
    
```php
    [!JotX? &action=`lastcomments` !] - Последние комментарии
```

### New settings.
* **notifyEmails** - subscribing to specific addresses
* **subjectEmails** - the header of the emails for this newsletter
* **subscriber** - the name of the recipient for this newsletter, if not specified (by default "subscriber")
* **tplNotifyEmails** - template for this newsletter

```php
    [!JotX? &notifyEmails=`user1@site.ru:Subscriber 1,user2@site.ru:Subscriber 2,user3@site.ru` !]
```

* **docids** - docid list, you can specify ranges
* **tagids** - list of tagid, separated by comma
* **userids** - a list of user ids, separated by commas. For web users - negative.
* **limit** - limit the number of comments

```php
    [!JotX? &action=`lastcomments` &limit=`10` !] - 10 latest comments from around the site
    [!JotX? &docids=`*` &sortby=`rand()` &limit=`1` !] - random comment from all over the site
    [!JotX? &docids=`1,2,5-10,20*,30-35,40**,` !] - and you can also :)
```
The docids and tagids parameters are used to output data, docid and tagid are used to enter current data, so they are separated

* **depth** - depth of tree comments (default 10)
* **upc** - how to count userpostcount (0 - do not count, 1 (default) - count for the whole site, 2 - count for the current page)

* **js and jsFile** - analogues of css and cssFile

Page-by-page navigation

* **tplNavPage** - template for page number design
* **tplNavPageCur** - template for designing the current page number
* **tplNavPageSpl** - page number separator
* **tplNavPageDots** - pagination break (ellipsis by default)
* **pageAdjacents** - number of pages before and after the current one (default 2)

### Events.
Each of the two classes has its own.

onBeforeConfiguration,onBeforeRunActions,onRunActions,onConfiguration,onBeforeFirstRun, onFirstRun,onSubscriptionCheck,onDeleteComment,onGetCommentFields,onBeforeSaveComment, onSaveComment,onGetSubscriptions,onBeforeGetSubscriptions,onBeforeGetUserInfo, onBeforeNotify,onBeforeSubscribe,onBeforeUnsubscribe,onBeforeValidateFormField, onValidateFormFieldFail,onBeforePOSTProcess,onProcessForm,onBeforeProcessPassiveActions, onProcessPassiveActions, onBeforeGetCommentCount,onBeforeGetComments,onGetComments, onReturnOutput,onSetDefaultOutput,onBeforeGetUserPostCount,onSetFormOutput,onSetCommentsOutput

### Plugins for events.
They can be loaded both from snippets and from files. Can be written separated by commas.

```php
    [!JotX? &onBeforeValidateFormField=`nolink,onlyrus` !]
```

The composition includes plugins:

* **subscribe** (events: onBeforeFirstRun,onSaveComment,onBeforeRunActions,onBeforeProcessPassiveActions,onGetSubscriptions,onBeforeGetUserInfo,onBeforeNotify) - subscription of site guests to notifications about new comments. Also need 2 fixes in the templates: checkbox and unsubscribe text, see the example in tree.config.php
* **ajax** (events: onSetCommentsOutput,onSetFormOutput,onReturnOutput) - loading only via ajax
* **antispam** (events: onBeforePOSTProcess,onSetFormOutput) - fight bots by adding a hidden trap field
* **nolink** (event: onBeforeValidateFormField) - disallow links in comments
* **onlyrus** (event: onBeforeValidateFormField) - ban non-Russian spam
* **notifyfaq** (events: onProcessForm,onBeforeNotify) - notification to the user about the answer to the question in the FAQ
* **rss** (events: onBeforeProcessPassiveActions,onSetCommentsOutput) - adds a link to the RSS feed
* **rating** (events: onFirstRun,onReturnOutput) - adds vote per comment

There will be others.

### Other fixes.
* Notification system merged and redesigned for PHPMailer
* Queries to the database have been optimized, including for the userpostcount. User fields are combined with comment fields.
* Fixed old bugs with deleting/adding fields
* Page-by-page pagination, in tree-like comments it also works if you include
* All sorts of little things, like engravers
