#!/bin/bash
clear
echo "═══════════════════════════════════════"
echo "🎮 SERVIDOR MINECRAFT BEDROCK"
echo "═══════════════════════════════════════"
echo ""

# Instalar dependências
echo "📦 Instalando dependências..."
apt-get update -qq > /dev/null 2>&1
apt-get install -y wget unzip > /dev/null 2>&1

# Baixar servidor
if [ ! -f "bedrock_server" ]; then
    echo "⬇️  Baixando Minecraft Bedrock Server..."
    wget -q --show-progress https://minecraft.azureedge.net/bin-linux/bedrock-server-1.21.50.07.zip
    echo "📂 Extraindo arquivos..."
    unzip -q bedrock-server-1.21.50.07.zip
    rm bedrock-server-1.21.50.07.zip
    chmod +x bedrock_server
fi

# Configurar servidor (MODO CRIATIVO, CHEATS ATIVADOS)
cat > server.properties << 'CONFIGEND'
server-name=§l§bServidor Bedrock
gamemode=creative
difficulty=easy
allow-cheats=true
max-players=20
online-mode=false
white-list=false
server-port=19132
server-portv6=19133
view-distance=32
tick-distance=6
player-idle-timeout=30
max-threads=8
level-name=Bedrock level
level-seed=
default-player-permission-level=operator
texturepack-required=false
content-log-file-enabled=false
compression-threshold=1
server-authoritative-movement=server-auth
player-movement-score-threshold=20
player-movement-distance-threshold=0.3
player-movement-duration-threshold-in-ms=500
correct-player-movement=false
server-authoritative-block-breaking=false
chat-restriction=None
disable-player-interaction=false
client-side-chunk-generation-enabled=true
block-network-ids-are-hashes=true
disable-persona=false
disable-custom-skins=false
server-build-radius-ratio=Disabled
CONFIGEND

# Criar permissões
cat > permissions.json << 'PERMEND'
[]
PERMEND

cat > allowlist.json << 'ALLOWEND'
[]
ALLOWEND

echo "✅ Servidor configurado com sucesso!"
echo ""
echo "═══════════════════════════════════════"
echo "⚙️  CONFIGURAÇÕES ATIVAS:"
echo "═══════════════════════════════════════"
echo "🎮 Modo: CRIATIVO"
echo "⭐ Cheats: ATIVADOS"
echo "👥 Max Jogadores: 20"
echo "🔓 Online Mode: DESATIVADO (sem login Xbox)"
echo "🌍 Distância de Visão: 32 chunks"
echo "🚪 Porta: 19132"
echo "═══════════════════════════════════════"
echo ""
echo "🚀 Iniciando servidor..."
echo "📡 Conecte-se usando o IP que aparecerá abaixo"
echo ""

# Iniciar servidor
LD_LIBRARY_PATH=. ./bedrock_server
