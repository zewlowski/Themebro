const { findByDisplayName } = require("@vendetta/metro");
const { instead } = require("@vendetta/patcher");
const { React, ReactNative: RN } = require("@vendetta/metro/common");

const BG_URL = "https://files.catbox.moe/is7fwe.mp4";

let unpatch;

module.exports = {
    onLoad() {
        const Chat = findByDisplayName("Chat") || findByDisplayName("MessagesConnected");
        if (!Chat) {
            console.warn("Chat component not found");
            return;
        }

        unpatch = instead("render", Chat, (args, orig) => {
            const content = orig(...args);
            return React.createElement(
                RN.View,
                { style: { flex: 1 } },
                React.createElement(RN.Image, {
                    source: { uri: BG_URL },
                    style: [RN.StyleSheet.absoluteFill, { opacity: 0.8 }],
                    resizeMode: "cover"
                }),
                content
            );
        });
    },
    onUnload() {
        if (unpatch) unpatch();
    }
};
