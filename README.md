# flutter_sticky_and_expandable_list

README i18n:[中文说明](https://raw.githubusercontent.com/tp7309/flutter_sticky_and_expandable_list/master/README_zh_CN.md)
![Screenshot](https://raw.githubusercontent.com/tp7309/flutter_sticky_and_expandable_list/master/doc/images/sliverlist.gif)

## Features

- Support build an expandable ListView, which can expand/collapse section group or pin section header.
- Use it with CustomScrollView、SliverAppBar.
- Listen the scroll offset of current sticky header,
  and current sticky header index.

## Getting Started

**Waiting Upload!!!**
In the `pubspec.yaml` of your flutter project, add the following dependency:

```yaml
dependencies:
  sticky_and_expandable_list: '^0.1.0'
```

## Basic Usage

```dart
    //sectionList is a custom data source for ExpandableListView.
    //echo section model must implement ExpandableListSection.
    var sectionList = MockData.getExampleSections();
    return ExpandableListView(
      builder: SliverExpandableChildDelegate<String, Section>(
          headerBuilder: (context, section, index) => Text("Header #$index"),
          itemBuilder: (context, section, item, index) => ListTile(
                leading: CircleAvatar(
                  child: Text("$index"),
                ),
                title: Text(item),
              )),
    );
```

[Detail Examples](https://github.com/tp7309/flutter_sticky_and_expandable_list/tree/master/example)

## FAQ

### How to expand/collapse item?

```dart
section.setSectionExpanded(true)
```

[Example](https://github.com/tp7309/flutter_sticky_and_expandable_list/tree/master/example/example_listview.dart)

### How to listen current sticky header or the sticky header scroll offset?

```dart
  @override
  Widget build(BuildContext context) {
    ExpandableListView(
      builder: SliverExpandableChildDelegate<String, Section>(
        headerController: _getHeaderController(),
      ),
    )
  }

  _getHeaderController() {
    var controller = ExpandableListHeaderController();
    controller.addListener(() {
      print("switchingSectionIndex:${controller.switchingSectionIndex}, stickySectionIndex:" +
          "${controller.stickySectionIndex},scrollPercent:${controller.percent}");
    });
    return controller;
  }
```
