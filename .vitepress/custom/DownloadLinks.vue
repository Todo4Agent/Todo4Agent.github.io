<script setup lang="ts">
import { VPLink } from 'vitepress/theme'

/** 下载入口：GitHub Releases（Windows / macOS / Linux 安装包） */
const releases = {
    label: 'GitHub Releases',
    href: 'https://github.com/Todo4Agent/Todo4Agent/releases',
}
</script>

<template>
    <div class="download-links">
        <VPLink class="download-links__item" :href="releases.href" target="_blank" rel="noopener noreferrer" no-icon>
            <span class="download-links__button">
                <span class="download-links__button-label">{{ releases.label }}</span>
                <svg class="download-links__button-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                    aria-hidden="true">
                    <path fill="currentColor"
                        d="M12 3a1 1 0 0 1 1 1v9.17l3.3-3.3a1 1 0 1 1 1.4 1.42l-5 5a1 1 0 0 1-1.4 0l-5-5a1 1 0 1 1 1.4-1.42l3.3 3.3V4a1 1 0 0 1 1-1Zm-7 15a1 1 0 0 1 1-1h12a1 1 0 1 1 0 2H6a1 1 0 0 1-1-1Z" />
                </svg>
            </span>
        </VPLink>
    </div>
</template>

<style scoped>
.download-links {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    gap: 16px;
    margin: 16px 0;
}

.download-links__item {
    display: inline-flex;
    flex-direction: column;
    gap: 6px;
    color: var(--vp-c-text-1);
    text-decoration: none;
}

.download-links__button {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    height: 40px;
    padding: 0 20px;
    border: 1px solid var(--vp-button-brand-border);
    border-radius: 20px;
    background: var(--vp-button-brand-bg);
    color: var(--vp-button-brand-text);
    font-size: 14px;
    font-weight: 600;
    transition: background-color 0.25s, color 0.25s, border-color 0.25s;
}

.download-links__item:hover .download-links__button {
    background: var(--vp-button-brand-hover-bg);
    color: var(--vp-button-brand-hover-text);
    border-color: var(--vp-button-brand-hover-border);
}

.download-links__button-icon {
    width: 16px;
    height: 16px;
}
</style>
