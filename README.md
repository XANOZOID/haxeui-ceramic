# HaxeUI Ceramic backend
- The cwd for `resources` and `@:build` xmls is `2` levels deep from project root. Add `../../` to your haxeui filepaths 
- Images can be loaded from your main scene asset object, the one you pass to toolkit.init or a `file://` path
	- If you want to use from an asset object, pass the file name to the haxeui prop
	- `<image resource="ceramic" />` at `assets` root (no file extension!)
	- `<image resource="icons/ceramic" />` where `icons` is a sub directory in the `assets` folder

## How to use
1) [Install ceramic](https://ceramic-engine.com/guides/install-ceramic/#install-ceramic)
2) Open an empty directory and run `ceramic init --name myproject` to create a blank project
3) Open the project in vscode
    - Install the [ceramic vscode extension](https://marketplace.visualstudio.com/items?itemName=jeremyfa.ceramic) if you haven't got it already
5) Run in the **same** project directory: 
```
haxelib git haxeui-core https://github.com/haxeui/haxeui-core
haxelib git haxeui-ceramic https://github.com/Jarrio/haxeui-ceramic
```
5) Add the following to your ceramic.yml
```
    libs:
        - haxeui-core
        - haxeui-ceramic
```
6) In your `Project.hx` `ready()` function initialise your haxeui things
```
//put the following code AFTER you call app.scenes.main = new MainScene()
Toolkit.init(); // some optional config can be passed to init
//Toolkit.theme = 'dark';
var haxeui_component = new MyComponent();
Screen.instance.addComponent(haxeui_component);
```

## Extra Features
### FPS Throttling
In your `Toolkit.init()` there's a new option called `performance` set this to `FPS` and whenever your app gets into an idle state, it will lower the FPS down to 15 and boost it back up when it is no longer idle
### Cached Rendering
Out of the box this will only update the UI when a change has occured to prevent constant draws to occur. If you want to completely turn this feature off add the `no_filter_root` define to your ceramic.yml.

If you want to use the feature but want to add non UI components to your UI hierarchy then here's what you do:
1) Add `import haxe.ui.backend.Ceramic;`
2) Then in your custom visual/component, call `Ceramic.render()`

so an example:

```hx
import haxe.ui.backend.Ceramic;

class Foo extends Visual {
	var updated:Bool = false;
	public function update() {
		if (!this.updated) {
			return;
		}
		// Do stuff
		Ceramic.forceRender(); //<-- Call this to force a complete UI re-render
	}
}
```
----
Not working/Bugged:

- canvas
- number stepper (text alignment)

Working:
basic 
- buttons
- button bar
- checkboxes
- option boxes
- progress bars
- sliders
- scrollbars
- classic scroll bars
- calendars
- labels
- drop down 
- dropdown
- switches

containers
- tabs
- frames
- scroll views
- table views
- accordian
- cards
- menus
- list view
- tables
- tree view

layouts
- absolute
- box
- horizontal
- vertial
- grid
- splitter
- spliter

misc
- tooltips
- drag
- animations
- clipping
- images

