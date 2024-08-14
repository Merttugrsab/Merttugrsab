let currentLocation = "orman";
let inventory = [];

function showLocation() {
  switch (currentLocation) {
    case "orman":
      console.log("Karanlık bir ormanın içinde buluyorsun kendini. Ağaçlar gökyüzünü kapatmış, etrafında sadece kuş sesleri duyabiliyorsun. Önünde iki yol görünüyor.");
      break;
    case "mağara":
      console.log("Karanlık ve nemli bir mağaraya giriyorsun. Duvarlarda garip şekiller ve taşlar var. Etrafında bir hışırtı duyabiliyorsun.");
      break;
    case "göl":
      console.log("Güneşli bir gölün kıyısına geliyorsun. Su berrak ve sakin, etrafında çiçekler açmış. Gölün ortasında küçük bir ada görünüyor.");
      break;
  }
}

function showInventory() {
  if (inventory.length === 0) {
    console.log("Çantan boş.");
  } else {
    console.log("Çantanın içinde şunlar var:");
    for (let i = 0; i < inventory.length; i++) {
      console.log(`${i + 1}. ${inventory[i]}`);
    }
  }
}

function playGame() {
  showLocation();
  showInventory();

  let command = prompt("Ne yapmak istiyorsun? (git, al, kullan, bak, çanta)");

  if (command === "git") {
    let direction = prompt("Hangi yöne gitmek istiyorsun? (sol, sağ)");
    switch (currentLocation) {
      case "orman":
        if (direction === "sol") {
          currentLocation = "mağara";
        } else if (direction === "sağ") {
          currentLocation = "göl";
        }
        break;
      case "mağara":
        if (direction === "sol") {
          currentLocation = "orman";
        }
        break;
      case "göl":
        if (direction === "sol") {
          currentLocation = "orman";
        }
        break;
    }
  } else if (command === "al") {
    switch (currentLocation) {
      case "mağara":
        if (inventory.includes("taş")) {
          console.log("Zaten bir taşın var.");
        } else {
          inventory.push("taş");
          console.log("Bir taş aldın.");
        }
        break;
      case "göl":
        if (inventory.includes("çiçek")) {
          console.log("Zaten bir çiçeğin var.");
        } else {
          inventory.push("çiçek");
          console.log("Bir çiçek aldın.");
        }
        break;
    }
  } else if (command === "kullan") {
    let item = prompt("Ne kullanmak istiyorsun? (taş, çiçek)");
    if (item === "taş" && inventory.includes("taş")) {
      if (currentLocation === "mağara") {
        console.log("Taşı mağaranın duvarına vurdun ve gizli bir geçit açıldı!");
        // Geçit açma eylemi için ek kod ekleyebilirsiniz
      } else {
        console.log("Burada taş kullanılamaz.");
      }
    } else if (item === "çiçek" && inventory.includes("çiçek")) {
      if (currentLocation === "göl") {
        console.log("Çiçeği suya attın ve gölde bir ejderha belirdi!");
        // Ejderha ile etkileşim için ek kod ekleyebilirsiniz
      } else {
        console.log("Burada çiçek kullanılamaz.");
      }
    } else {
      console.log("Bu eşyayı kullanamazsın.");
    }
  } else if (command === "bak") {
    switch (currentLocation) {
      case "mağara":
        console.log("Duvarlarda garip şekiller ve taşlar var.");
        break;
      case "göl":
        console.log("Su berrak ve sakin, etrafında çiçekler açmış.");
        break;
    }
  } else if (command === "çanta") {
    showInventory();
  } else {
    console.log("Geçersiz komut.");
  }

  playGame();
}

playGame();
