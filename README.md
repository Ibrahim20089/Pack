import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.plugin.java.JavaPlugin;

public class FlyPlugin extends JavaPlugin {
    @Override
    public void onEnable() {
        // Plugin aktivieren
    }

    @Override
    public void onDisable() {
        // Plugin deaktivieren
    }

    @Override
    public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
        if (command.getName().equalsIgnoreCase("fly")) {
            if (sender instanceof Player) {
                Player player = (Player) sender;
                if (player.hasPermission("flyplugin.fly")) {
                    boolean isFlying = player.getAllowFlight();
                    player.setAllowFlight(!isFlying);
                    player.setFlying(!isFlying);
                    
                    String flyStatus = isFlying ? "deaktiviert" : "aktiviert";
                    player.sendMessage("Flugmodus " + flyStatus + ".");
                    return true;
                } else {
                    player.sendMessage("Du hast nicht die Berechtigung, um zu fliegen.");
                    return true;
                }
            } else {
                sender.sendMessage("Dieser Befehl kann nur von einem Spieler ausgeführt werden.");
                return true;
            }
        }
        return false;
    }
}
