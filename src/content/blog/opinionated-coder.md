---
title: "Opinionated Coder Kick-off"
description: "What is opinionated coder"
pubDate: "Dec 28 2023"
heroImage: "/opinionated-coder.webp"
tags: ["kick-off"]
---
## A new blog in 2024? Just... why?

It doesn't make sense. Create a new blog in 2024 does not make any sense, I know, but I felt the compelling 
need to make a new start where to put my ideas in order and continuously keep track of my thoughts, 
researches, discussions with friends.

So the motivation is mostly personal with the advantage that, by writing in a public place (even if nobody 
will ever read it), I will feel the responsibility to commit to my projects with more dedication and continuity.

Another 

```java
package org.fuin.cqrs4j.example.quarkus.shared;

import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Inject;
import org.eclipse.microprofile.config.inject.ConfigProperty;

import java.net.MalformedURLException;
import java.net.URL;

/**
 * Application configuration.
 */
@ApplicationScoped
public class Config {

    private static final String EVENT_STORE_PROTOCOL = "http";

    private static final String EVENT_STORE_HOST = "127.0.0.1";

    private static final int EVENT_STORE_HTTP_PORT = 2113;

    private static final String EVENT_STORE_USER = "admin";

    private static final String EVENT_STORE_PASSWORD = "changeit";

    @Inject
    @ConfigProperty(name = "EVENT_STORE_PROTOCOL", defaultValue = EVENT_STORE_PROTOCOL)
    private String eventStoreProtocol;

    @Inject
    @ConfigProperty(name = "EVENT_STORE_HOST", defaultValue = EVENT_STORE_HOST)
    String eventStoreHost;

    @Inject
    @ConfigProperty(name = "EVENT_STORE_HTTP_PORT", defaultValue = "" + EVENT_STORE_HTTP_PORT)
    int eventStoreHttpPort;

    @Inject
    @ConfigProperty(name = "EVENT_STORE_USER", defaultValue = EVENT_STORE_USER)
    String eventStoreUser;

    @Inject
    @ConfigProperty(name = "EVENT_STORE_PASSWORD", defaultValue = EVENT_STORE_PASSWORD)
    String eventStorePassword;

    /**
     * Constructor using default values internally.
     */
    public Config() {
        super();
        this.eventStoreProtocol = EVENT_STORE_PROTOCOL;
        this.eventStoreHost = EVENT_STORE_HOST;
        this.eventStoreHttpPort = EVENT_STORE_HTTP_PORT;
        this.eventStoreUser = EVENT_STORE_USER;
        this.eventStorePassword = EVENT_STORE_PASSWORD;
    }

    /**
     * Constructor with all data.
     *
     * @param eventStoreProtocol
     *            Protocol (http or https).
     * @param eventStoreHost
     *            Host.
     * @param eventStoreHttpPort
     *            HTTP port
     * @param eventStoreUser
     *            User.
     * @param eventStorePassword
     *            Password.
     */
    public Config(final String eventStoreProtocol, final String eventStoreHost, final int eventStoreHttpPort, final String eventStoreUser,
                  final String eventStorePassword) {
        super();
        this.eventStoreProtocol = eventStoreProtocol;
        this.eventStoreHost = eventStoreHost;
        this.eventStoreHttpPort = eventStoreHttpPort;
        this.eventStoreUser = eventStoreUser;
        this.eventStorePassword = eventStorePassword;
    }

    /**
     * Returns the protocol of the event store.
     *
     * @return Protocol.
     */
    public String getEventStoreProtocol() {
        return eventStoreProtocol;
    }

    /**
     * Returns the host name of the event store.
     *
     * @return Name.
     */
    public String getEventStoreHost() {
        return eventStoreHost;
    }

    /**
     * Returns the HTTP port of the event store.
     *
     * @return Port.
     */
    public int getEventStoreHttpPort() {
        return eventStoreHttpPort;
    }

    /**
     * Returns the username of the event store.
     *
     * @return Username.
     */
    public String getEventStoreUser() {
        return eventStoreUser;
    }

    /**
     * Returns the password of the event store.
     *
     * @return Password.
     */
    public String getEventStorePassword() {
        return eventStorePassword;
    }

    /**
     * Creates a URL with parameters from the config.
     *
     * @return Event store base URL.
     */
    public URL getEventStoreURL() {
        try {
            return new URL("http", eventStoreHost, eventStoreHttpPort, "/");
        } catch (final MalformedURLException ex) {
            throw new RuntimeException("Failed to create event store URL", ex);
        }
    }

}

```