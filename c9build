define(function(require, exports, module) {
    main.consumes = ["Plugin", "commands", "tabManager", "terminal", "menus", "ui"];
    main.provides = ["myplugin"];
    return main;

    function main(options, imports, register) {
        //定义插件的基本组件
        var Plugin = imports.Plugin;
        var commands = imports.commands;
        var menus = imports.menus;
        var ui = imports.ui;

        /***** Initialization *****/
        // 插件初始化
        var plugin = new Plugin("Ajax.org", main.consumes);
        var emit = plugin.getEmitter();
        //load()方法，启动时自动加载。
        function load() {
            //新建一个命令，命名为test ,
            // bindKey:绑定按键，mac系统command+Alt+J ,win系统 Ctrl-Alt-J ，
            //exec 执行内容是弹出一个success 的显示，
            //isAvailable：方法是否可用，可以自定义些限制条件,这里返回一个true
            commands.addCommand({
                name: "test",
                bindKey: { mac: "Command-Alt-J", win: "Ctrl-Alt-J" },
                exec: function() {
                    alert("success!");
                },
                isAvailable: function() { return true; }
            }, plugin);

            //添加工具栏 在menu /tools下会多出一个Item01的菜单。
            menus.addItemByPath("Tools/Wanghao", new ui.item({
                command: "test"
            }), 300, plugin);
        }

        /***** Methods *****/



        /***** Lifecycle *****/
        //插件的生命周期有两个事件，加载和加载结束，这里将load()绑定到load的生命周期内。
        plugin.on("load", function() {
            load();
        });
        plugin.on("unload", function() {

        });

        /***** Register and define API *****/
        //注册和定义插件。
        plugin.freezePublicAPI({

        });

        register(null, {
            "myplugin": plugin
        });
    }
});
